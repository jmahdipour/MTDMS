# TB-016 — ISO 6892-1 Strain Reference Point, L0/Lc Handling & Strain-Origin Normalization Specification

**Document:** TB-016  
**Project:** MTDMS — Material Test Data Management System  
**Version:** 1.0  
**Status:** Approved / Frozen  
**Parent:** TB-005 → TB-015  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in  
**Calculation model:** Array-Based

## 1. Purpose

TB-016 defines strain reference and strain-origin handling, especially when the approved source sequence is Crosshead → Extensometer → Crosshead.

## 2. Metadata Scope

Only these metadata rows are used at this stage:

```text
10 : d/a
11 : b
13 : L0
```

Other metadata is ignored by this specification.

## 3. L0

`L0` is read from metadata row 13 and is not inferred from Displacement.

## 4. Reference Point

Each strain segment has a traceable reference containing DatasetIndex, Source, Displacement, Deformationt and ReferenceLength.

Reference Point is an independent analytical concept and is not automatically identical to Test Start or Extensometer Attach.

## 5. Crosshead Reference

Where the applicable Method uses Crosshead strain:

```text
CrossheadStrain(i) = (Displacement(i) - CrossheadReferenceDisplacement) / L0
```

## 6. Extensometer Reference

Where the applicable Method uses Extensometer strain:

```text
ExtensometerStrain(i) = (Deformationt(i) - ExtensometerReferenceDeformation) / L0
```

Use of another reference length requires an explicit Method rule.

## 7. Deformationt

`Deformationt` is a valid Extensometer measurement only while `StrainSource = EXTENSOMETER`. A zero value alone does not prove disconnection, and a non-zero value alone does not prove connection.

## 8. Source States

```text
CROSSHEAD
EXTENSOMETER
INVALID
```

The source state is supplied by the approved segmentation/event engine.

## 9. Source Segmentation

A test may contain:

```text
Segment 1: CROSSHEAD
Segment 2: EXTENSOMETER
Segment 3: CROSSHEAD
```

These segments remain separately traceable.

## 10. Unified Strain

A derived `EngineeringStrain()` array may be constructed from the source-specific arrays. Each point retains DatasetIndex, StrainSource and SegmentID.

## 11. Transition Continuity

At Extensometer Attach and Release, continuity must be checked. The engine must not silently create an artificial connection or hide a scale/reference discontinuity.

## 12. Attach Event

`ExtensometerAttachEvent` identifies the transition into the Extensometer source state. Boundary inclusion rules must be explicit and must not duplicate a Dataset point.

## 13. Release Event

`ExtensometerReleaseEvent` identifies the transition back to Crosshead. Release does not automatically create a new strain origin.

## 14. Post-Release Crosshead

Post-release Crosshead strain requires a defined reference/offset strategy so that a false strain jump is not introduced.

A derived offset may be applied:

```text
CorrectedCrossheadStrain(i) = CrossheadStrainRaw(i) + StrainOffset
```

`StrainOffset` must be calculated and traceable.

## 15. Segment Offset

Each offset retains SegmentID, Source, ReferenceIndex, OffsetValue and CalculationVersion.

## 16. Raw vs Derived

Raw arrays:

```text
CrossheadStrainRaw()
ExtensometerStrainRaw()
```

are distinct from:

```text
EngineeringStrain()
CorrectedGraphStrain()
```

Raw values are never overwritten.

## 17. Reference Strategies

Supported conceptual strategies are:

```text
TEST_START_REFERENCE
ATTACH_REFERENCE
METHOD_DEFINED_REFERENCE
```

The applicable Method selects the strategy.

## 18. Test Start Reference

If a Method explicitly defines Test Start as the strain reference, the relevant derived strain may use TestStartIndex. TB-016 does not impose this as a universal rule.

## 19. Attach Reference

If the Method defines Attach as Extensometer reference:

```text
ExtensometerStrain(i) = (Deformationt(i) - Deformationt(AttachIndex)) / L0
```

## 20. Release Reference

Release is not equivalent to a new zero unless explicitly defined by the applicable Method.

## 21. Array Alignment

All arrays remain aligned by DatasetIndex:

```text
DatasetIndex(i)
↕ Force(i)
↕ Displacement(i)
↕ Deformationt(i)
↕ StrainSource(i)
↕ EngineeringStrain(i)
```

## 22. No Sorting

Strain arrays are never independently sorted.

## 23. No Automatic Interpolation

Source transitions are not automatically interpolated or smoothed. Any interpolation must be an explicit Method/View operation.

## 24. Invalid Extensometer Data

Invalid `Deformationt` during an Extensometer source state must not cause a silent switch to Crosshead. The state becomes invalid or the explicit Method rule is applied.

## 25. Manual Correction

Operator strain-reference or offset changes are stored as `ManualStrainCorrectionEvent` with DatasetIndex, OldValue, NewValue, CorrectionType, Operator, Timestamp, Reason and Comment.

## 26. Calculation Version

Changing reference or offset creates a new CalculationVersion so previous results remain distinguishable.

## 27. Graph Correction

Graph-only correction uses a separate `CorrectedGraphStrain()` array and does not silently replace calculation strain.

## 28. L0 vs Post-Fracture Gauge Length

`L0` is the initial gauge length. Post-fracture measured gauge length is a separate value used by TB-010 for elongation after fracture.

```text
L0 ≠ L_after
```

## 29. Lc

If a Method/Standard requires `Lc`, it is stored independently from L0. It must not be guessed from unspecified metadata rows.

```text
L0 ≠ Lc
```

unless the applicable geometry/standard explicitly establishes equality.

## 30. Post-Fracture Elongation

TB-010 remains responsible for post-fracture elongation. Conceptually:

```text
A% = ((L_after - L0) / L0) × 100
```

This result does not replace the pre-fracture engineering strain array.

## 31. Relationship to Other Blueprints

```text
TB-005 → Source Segmentation
TB-016 → Reference / Origin / Segment Offset
TB-013 → Engineering Curve
TB-011 → Young's Modulus
TB-008 → Rp0.2
TB-010 → Post-Fracture Elongation / Graph Axis Correction
```

## 32. Freeze Decisions

| ID | Decision |
|---|---|
| D-271 | L0 is read from metadata row 13. |
| D-272 | Only metadata rows 10, 11 and 13 are used at this stage. |
| D-273 | L0 and Lc are independent concepts. |
| D-274 | Zero Point, Test Start, Attach and Reference are independent Events/concepts. |
| D-275 | Crosshead and Extensometer are independent source segments. |
| D-276 | Deformationt is a valid Extensometer source only when StrainSource=EXTENSOMETER. |
| D-277 | Deformationt=0 alone does not determine Extensometer connection state. |
| D-278 | Release does not automatically create a new strain origin. |
| D-279 | Segment Offset is a derived, traceable value. |
| D-280 | Raw Displacement and Raw Deformationt are never overwritten. |
| D-281 | EngineeringStrain is a Derived Array. |
| D-282 | Every engineering strain point retains DatasetIndex and StrainSource. |
| D-283 | Source transitions do not silently interpolate or smooth. |
| D-284 | A DatasetIndex cannot be duplicated in the Curve Dataset. |
| D-285 | Invalid Extensometer data does not silently switch to Crosshead. |
| D-286 | Manual strain correction is recorded as an Event. |
| D-287 | Reference/Offset changes create a new CalculationVersion. |
| D-288 | L_after is independent of EngineeringStrain. |
| D-289 | Graph correction and calculation strain are independent. |
| D-290 | All strain arrays remain aligned by DatasetIndex. |

## 33. Status

**Approved / Frozen — TB-016.**
