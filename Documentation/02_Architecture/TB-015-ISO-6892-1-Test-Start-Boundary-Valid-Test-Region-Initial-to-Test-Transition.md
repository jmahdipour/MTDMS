# TB-015 — ISO 6892-1 Test Start Boundary, Valid Test Region & Initial-to-Test Transition Specification

**Document:** TB-015  
**Project:** MTDMS — Material Test Data Management System  
**Version:** 1.0  
**Status:** Approved / Frozen  
**Parent:** TB-005 → TB-014  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in  
**Calculation model:** Array-Based

## 1. Purpose

TB-015 defines the analytical boundary between the initial portion of the TXT Dataset and the Valid Test Region. No Raw Dataset row is deleted.

## 2. Test Start

`TestStartIndex` is an analytical boundary identifying the point from which the selected Method considers the test region valid. It is not a physical deletion point.

## 3. First Row Rule

The first file row is not automatically Test Start. The first non-zero force is also not automatically Test Start.

## 4. Raw Dataset

All rows remain available:

```text
Initial
Seating
Preload
Pre-Test
Valid Test
Post-Test
```

## 5. Valid Test Region

```text
ValidTestRegion
├── StartIndex
├── EndIndex
└── DetectionSource
```

`StartIndex = TestStartIndex`.

The End Index is controlled by the applicable Method and later boundaries such as Fracture.

## 6. Initial-to-Test Transition

Test Start is an independent Event separating the initial/conditioning region from the valid test region.

## 7. Event Independence

The following remain independent:

```text
ZeroPointEvent
PreloadEvent
TestStartEvent
ExtensometerAttachEvent
ExtensometerReleaseEvent
YieldEvent
RmEvent
FractureEvent
```

The project must not assume that every test has identical Event ordering.

## 8. TestStartEvent

The event retains:

```text
DatasetIndex
DetectionSource
Operator
Timestamp
Reason
Comment
```

## 9. DetectionSource

Allowed values:

```text
AUTOMATIC
MANUAL
METHOD_DEFINED
```

## 10. Automatic Detection

Automatic detection may use Force, Displacement, Time, slope, rate, stability and other Dataset characteristics, but the exact detection rule is Method/Configuration driven.

## 11. Thresholds

Force, Displacement, or Time thresholds may be used only when explicitly configured. Threshold values must not be hard-coded.

## 12. Candidate Start Region

Automatic detection may first identify a candidate region rather than using the first threshold crossing:

```text
TestStartCandidate
├── StartIndex
├── EndIndex
├── Score
├── DetectionRule
└── Confidence
```

## 13. Noise Protection

Threshold-based detection may use configurable hysteresis and/or stability requirements so temporary noise does not create a false Test Start.

## 14. Manual Selection

An operator may select Test Start on the graph. The screen coordinate is mapped to a Dataset Index; calculations use the Dataset Index, not pixels.

## 15. Manual Override

When automatic detection exists, the automatic index remains preserved and the manual index is stored as an override.

Audit information includes:

```text
OldIndex
NewIndex
Operator
Timestamp
Reason
Comment
```

## 16. TestStart and Strain

If the applicable Method defines Test Start as the strain reference, derived strain arrays may use the Test Start reference. For example:

```text
EngineeringStrain(i) = (Displacement(i) - Displacement(TestStartIndex)) / L0
```

For an Extensometer source, the corresponding reference may be defined by the Method. TB-015 does not impose one universal formula for every Method.

## 17. Crosshead Source

For Crosshead-based strain, the reference displacement is Method-defined and must remain traceable.

## 18. Extensometer Source

For Extensometer-based strain, `Deformationt` is used only while the approved strain-source state is EXTENSOMETER. Its reference point is Method-defined.

## 19. TestStart vs Extensometer Attach

```text
TestStartIndex ≠ ExtensometerAttachIndex
```

They remain independent even when their indices happen to be equal in a particular test.

## 20. TestStart vs Yield

```text
TestStartIndex ≠ YieldIndex
```

## 21. TestStart vs Preload

```text
TestStartIndex ≠ PreloadIndex
```

## 22. Valid Boundary Ordering

For a conventional tensile test the expected logical ordering is generally:

```text
TestStart ≤ Yield ≤ Rm ≤ Fracture
```

An unexpected ordering produces a Boundary Consistency Warning/Invalid Status as appropriate. The system must not silently rearrange indices.

## 23. Initial Data After Test Start

Earlier rows remain in Raw Dataset. Only `RowPhase`, `CalculationEligible`, and derived/view states may change.

## 24. Effect on Downstream Methods

TB-015 supplies Test Start information to downstream methods:

```text
TB-011 → Young's Modulus / Elastic Region
TB-008 → Rp0.2
TB-009 → Rm / Fracture
TB-010 → Elongation / Axis Correction
TB-013 → Engineering Curve
```

Each method remains responsible for its own calculation rules.

## 25. Recalculation

Changing Test Start triggers rebuilding of affected derived arrays and recalculation of dependent Method results. Raw arrays remain unchanged.

## 26. Array Integrity

Raw arrays remain parallel:

```text
Length(No)
= Length(Time)
= Length(Displacement)
= Length(Deformationt)
= Length(Force)
```

Derived arrays must preserve Dataset Index traceability.

## 27. Graph Analysis Overlay

Graph Analysis may show:

```text
Initial Region
Seating
Preload
Test Start
Extensometer Attach
Extensometer Release
Yield
Rm
Fracture
```

These are overlays and do not modify the calculation arrays.

## 28. Final Report

Analysis overlays are excluded from the final report by default. Approved result values and configured traceability fields may be reported.

## 29. Data Lineage

Every Test Start result must be traceable:

```text
Result
 ↓
Method Run
 ↓
TestStartIndex
 ↓
Normalized Dataset
 ↓
Raw TXT Row
```

## 30. Freeze Decisions

| ID | Decision |
|---|---|
| D-251 | TestStart is an independent analytical boundary. |
| D-252 | The first file row is not automatically Test Start. |
| D-253 | First Non-Zero Force is not automatically Test Start. |
| D-254 | TestStart, Preload and ZeroPoint are independent Events. |
| D-255 | TestStart and Extensometer Attach are independent. |
| D-256 | TestStart and Yield are independent. |
| D-257 | Automatic Detection is Method/Configuration driven. |
| D-258 | Thresholds are not hard-coded. |
| D-259 | Candidate Start Regions may be used to protect against noise. |
| D-260 | Hysteresis/Stability, when used, is configurable. |
| D-261 | Manual TestStart maps to DatasetIndex. |
| D-262 | Pixel coordinates never enter numerical calculations. |
| D-263 | Manual override preserves the automatic result. |
| D-264 | Changing TestStart triggers recalculation of affected derived arrays/results. |
| D-265 | Raw Dataset never changes during recalculation. |
| D-266 | Invalid boundary ordering produces Warning/Invalid Status, not silent correction. |
| D-267 | TestStart may be a strain reference only when defined by the applicable Method. |
| D-268 | TestStart is available to TB-011, TB-008, TB-009, TB-010 and TB-013 as an analytical boundary. |
| D-269 | ValidTestRegion starts at TestStart and ends at the Method-defined terminal boundary. |
| D-270 | Traceability from Test Start to the original TXT row is mandatory. |

## 31. Status

**Approved / Frozen — TB-015.**
