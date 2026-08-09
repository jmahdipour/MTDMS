# TB-018 — ISO 6892-1 Engineering Strain Calculation, Crosshead/Extensometer Source Integration & Strain Array Validation Specification

**Document:** TB-018  
**Project:** MTDMS — Material Test Data Management System  
**Version:** 1.0  
**Status:** Approved / Frozen  
**Parent:** TB-005 → TB-017  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in  
**Calculation model:** Array-Based

## 1. Purpose

TB-018 defines construction of the Engineering Strain array from the exported TXT dataset and supports the approved source sequence:

```text
CROSSHEAD
EXTENSOMETER
CROSSHEAD
```

Raw Dataset values are never changed. Engineering Strain is always a Derived Array.

## 2. Inputs

```text
DatasetIndex()
Time()
Displacement()
Deformationt()
Force()
L0
StrainSource()
SegmentID()
TestStartIndex
ExtensometerAttachIndex
ExtensometerReleaseIndex
```

## 3. Strain Source

For every DatasetIndex:

```text
CROSSHEAD
EXTENSOMETER
INVALID
```

The source state comes from the Event/Segmentation Engine and is not inferred from the numerical value of Deformationt alone.

## 4. Segment Model

A test may contain:

```text
Segment 1: CROSSHEAD
Segment 2: EXTENSOMETER
Segment 3: CROSSHEAD
```

Every segment retains SegmentID, Source, StartIndex, EndIndex, ReferenceIndex, ReferenceValue and Offset.

## 5. Engineering Strain

```text
EngineeringStrain = ΔL / L0
```

where L0 is the approved initial gauge/reference length.

## 6. Crosshead Strain

```text
CrossheadStrainRaw(i)
= (Displacement(i) - CrossheadReferenceDisplacement) / L0
```

The reference is determined by the applicable Method.

## 7. Extensometer Strain

```text
ExtensometerStrainRaw(i)
= (Deformationt(i) - ExtensometerReferenceDeformation) / L0
```

An alternative reference length is permitted only when explicitly defined by the applicable Method.

## 8. L0

L0 is obtained from approved Metadata/Geometry. It must not be guessed from Displacement, Deformationt, Test Start or Fracture.

## 9. Reference Point

Reference Point is independent from Test Start, Attach and Release Events unless the Method explicitly defines them as identical.

## 10. Crosshead-only Test

When Crosshead is the approved source for the valid region:

```text
EngineeringStrain(i) = CrossheadStrainRaw(i)
```

## 11. Extensometer-only Test

When Extensometer covers the approved valid region:

```text
EngineeringStrain(i) = ExtensometerStrainRaw(i)
```

provided the Extensometer data are valid.

## 12. Combined Source Test

For:

```text
CROSSHEAD → EXTENSOMETER → CROSSHEAD
```

three independent Raw Strain segments are generated and then reconciled into a Derived `EngineeringStrain()` array.

## 13. Attach Event

`ExtensometerAttachEvent` defines the transition from Crosshead to Extensometer. It is independent from TestStart.

## 14. Release Event

`ExtensometerReleaseEvent` defines the transition from Extensometer back to Crosshead. Release does not automatically create a new strain origin.

## 15. Continuity

At source transitions, continuity must be evaluated. A reference or scale discontinuity must be reported rather than hidden by changing Raw data.

## 16. Segment Offset

If the applicable Method permits continuity reconciliation:

```text
CorrectedSegmentStrain(i)
= RawSegmentStrain(i) + SegmentOffset
```

SegmentOffset must be derived, traceable and versioned.

## 17. Offset Restrictions

The engine must not automatically create an Offset merely because two source values differ. Offset application requires an explicit Method/Analysis rule.

## 18. Zero Point

ZeroPoint is independent from StrainReference. It may be used only where the applicable Method defines it as the reference.

## 19. Preload

Preload is independent from StrainReference. Preload presence alone does not establish the Strain Origin.

## 20. Initial Region

Initial, seating, preload and transition rows remain in Raw Dataset. Calculation eligibility is represented by flags and boundaries, not by deleting rows.

## 21. Invalid Strain

If `StrainSource=INVALID`:

```text
EngineeringStrain(i) = NA
```

while DatasetIndex, Force, Displacement and Deformationt remain preserved.

## 22. Missing Extensometer Data

When Source=EXTENSOMETER and Deformationt is missing/invalid, the engine must not silently switch to Crosshead. The row/segment becomes invalid or the explicit Method rule is applied.

## 23. Zero Deformationt

`Deformationt=0` does not by itself prove that the Extensometer is disconnected.

## 24. Boundary Inclusion

Segment boundary rules must prevent duplicate DatasetIndex values in the Unified Curve. A boundary may belong to one segment only according to the configured rule.

## 25. Gap

If a gap exists between source segments, `GapDetected=True`. The engine must not silently interpolate it.

## 26. Dataset Integrity

For the Unified Curve:

```text
Length(DatasetIndex)
= Length(EngineeringStrain)
= Length(StrainSource)
= Length(SegmentID)
```

For Raw arrays:

```text
Length(Force)
= Length(Displacement)
= Length(Deformationt)
```

## 27. Dataset Ordering

DatasetIndex remains in file order. Engineering Strain, Force and other arrays must never be independently sorted.

## 28. Smoothing

TB-018 does not apply smoothing. Any smoothing belongs to a separate Analysis Layer and must be explicit and traceable.

## 29. Interpolation

TB-018 does not automatically interpolate source transitions. Any interpolation must be explicitly authorized by the applicable Method.

## 30. Transition Quality

Each transition may be classified as:

```text
VALID
WARNING
INVALID
```

based on continuity, missing data, gaps, offset rules and Method requirements.

## 31. Manual Source Correction

Operator source changes are represented by `ManualSourceCorrectionEvent`, retaining OldSource, NewSource, StartIndex, EndIndex, Operator, Timestamp, Reason and Comment.

## 32. Manual Reference Correction

Operator reference changes are represented by `ManualReferenceCorrectionEvent`, retaining old/new reference index and value plus operator, timestamp and reason.

## 33. Raw Data Protection

Manual source, reference or offset corrections never modify Raw TXT values.

## 34. Calculation Version

Changes affecting Strain, including Source Segment, Reference, Offset or L0, create a new CalculationVersion.

## 35. Recalculation Dependencies

A valid Strain change may require recalculation of:

```text
Engineering Curve
Young's Modulus
Rp0.2
Yield-dependent results
Rm/Fracture-dependent results where applicable
Elongation-dependent results where applicable
```

## 36. Stress Integration

TB-017 produces `EngineeringStress()`. TB-018 produces `EngineeringStrain()`. The final engineering curve pairs both arrays by the same DatasetIndex.

## 37. Pair Integrity

For each valid curve point:

```text
EngineeringStress(i)
↔ EngineeringStrain(i)
↔ DatasetIndex(i)
```

No independent filtering or sorting is permitted.

## 38. Valid Test Region

Only the Method-defined Valid Test Region is used for standard calculations. TB-015 supplies the Test Start boundary and TB-009 supplies terminal boundaries.

## 39. Yield / Rp0.2

TB-006 determines Yield methodology and TB-008 calculates Rp0.2. TB-018 provides the source-aware Engineering Strain array required by those methods.

## 40. Approved Project Scenario

For the approved scenario:

```text
Extensometer active through Yield
        ↓
Extensometer Release
        ↓
Crosshead becomes source
```

The Extensometer segment ends at Release and is not extended beyond Release.

## 41. Rp0.2 Dependency

Because Rp0.2 depends on strain offset, Source and Reference segmentation must be resolved before Rp0.2 calculation.

## 42. Rm

TB-009 defines the valid Rm boundary. TB-018 preserves Source and Segment information so the Method can determine the applicable strain source without ambiguity.

## 43. Fracture

Fracture defines a terminal analytical boundary. TB-018 does not change Source solely because Force decreases.

## 44. Post-Fracture Elongation

TB-010 handles post-fracture gauge length and elongation. `L_after` is independent from L0 and the pre-fracture Engineering Strain array.

## 45. Horizontal Axis Correction

Graph-only correction is represented by a separate `CorrectedGraphStrain()` array and does not overwrite calculation strain.

## 46. Calculation vs Graph

```text
CalculationStrain
```

and

```text
GraphCorrectedStrain
```

are independent. If no correction exists, the graph array may equal the calculation array.

## 47. Traceability

```text
EngineeringStrain
 ↓
SegmentID
 ↓
StrainSource
 ↓
DatasetIndex
 ↓
Original TXT Row
```

## 48. Architecture

```text
RAW TXT
   ↓
Dataset Builder
   ↓
Event / Source Engine
   ↓
CROSSHEAD / EXTENSOMETER / CROSSHEAD
   ↓
Raw Strain Segments
   ↓
Reference / Offset Engine
   ↓
EngineeringStrain()
   ↓
Valid Test Region
   ↓
ISO 6892-1 Method Engine
```

## 49. Freeze Decisions

| ID | Decision |
|---|---|
| D-316 | Engineering Strain is a Derived Array. |
| D-317 | Raw Dataset is never modified to construct Strain. |
| D-318 | Crosshead and Extensometer are independent Strain Sources. |
| D-319 | Crosshead → Extensometer → Crosshead is represented by independent source segments. |
| D-320 | TestStart, Attach, Release and Reference are independent Events/concepts. |
| D-321 | L0 is the approved initial gauge/reference length. |
| D-322 | L0 is not inferred from Displacement or Deformationt. |
| D-323 | Deformationt is used as Strain source only when StrainSource=EXTENSOMETER. |
| D-324 | Deformationt=0 alone does not determine connection state. |
| D-325 | Release does not automatically create a new Strain Origin. |
| D-326 | Source transitions do not silently switch source. |
| D-327 | Source transitions do not silently interpolate. |
| D-328 | Source transitions do not silently smooth. |
| D-329 | A DatasetIndex appears at most once in the Unified Curve. |
| D-330 | Stress and Strain are paired by the same DatasetIndex. |
| D-331 | Source, SegmentID and DatasetIndex are retained for every Strain point. |
| D-332 | Manual Source/Reference corrections are recorded as Events. |
| D-333 | Manual corrections never modify Raw Dataset. |
| D-334 | Changes to L0, Reference, Offset or Source create a new CalculationVersion. |
| D-335 | Graph Correction and Calculation Strain are independent. |
| D-336 | Rp0.2 uses the validated Engineering Stress/Strain arrays. |
| D-337 | In the approved project scenario Extensometer remains active through Yield and Crosshead becomes source after Release. |
| D-338 | The Extensometer segment ends at Release. |
| D-339 | Post-Fracture Elongation is managed by TB-010. |
| D-340 | All Strain arrays remain DatasetIndex-aligned. |

## 50. Status

**Approved / Frozen — TB-018.**
