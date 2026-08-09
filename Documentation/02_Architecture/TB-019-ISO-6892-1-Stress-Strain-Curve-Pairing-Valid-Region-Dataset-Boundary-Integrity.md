# TB-019 — ISO 6892-1 Stress–Strain Curve Pairing, Valid Region Filtering & Dataset Boundary Integrity Specification

**Document:** TB-019  
**Project:** MTDMS — Material Test Data Management System  
**Version:** 1.0  
**Status:** Approved / Frozen  
**Parent:** TB-005 → TB-018  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in  
**Calculation model:** Array-Based

## 1. Purpose

TB-019 defines the final analytical dataset layer before the ISO 6892-1 Method Engine. It pairs Engineering Stress and Engineering Strain by the same DatasetIndex, applies valid-region and eligibility rules, and preserves all raw rows and original ordering.

## 2. Core Principle

Filtering applies only to a Derived/Analysis Dataset. Raw Dataset is immutable and is never deleted, sorted, re-indexed, or overwritten.

## 3. Inputs

```text
DatasetIndex()
Time()
ForceN()
EngineeringStress()
EngineeringStrain()
StrainSource()
SegmentID()
TestStartIndex
TerminalIndex
FractureIndex
CalculationEligible()
```

## 4. Output

`ValidCurveDataset()` contains, at minimum:

```text
DatasetIndex
Time
ForceN
EngineeringStress
EngineeringStrain
StrainSource
SegmentID
```

## 5. DatasetIndex

DatasetIndex is the primary relationship key for all arrays. Stress and Strain are paired only when they refer to the same DatasetIndex.

## 6. CurvePoint

A CurvePoint is one entity:

```text
CurvePoint
├── DatasetIndex
├── Stress
├── Strain
├── Time
├── Force
├── StrainSource
└── SegmentID
```

Stress and Strain must not be managed as unrelated lists.

## 7. Missing Values

Missing/invalid Stress or Strain makes the corresponding CurvePoint invalid for Method calculation, while the original Raw Dataset row remains preserved.

`Missing ≠ 0`.

## 8. Zero Values

A valid point with Stress=0 and Strain=0 is not removed merely because the values are zero.

## 9. Test Start

TB-015 supplies TestStartIndex. Rows before the applicable Test Start boundary may contain preload, seating, zeroing or initial movement and are excluded from the Method Dataset according to the configured boundary rule, without deleting Raw rows.

## 10. Terminal Boundary

The analytical end boundary is supplied by the applicable Method/Event Engine. TB-019 consumes the boundary and does not independently redefine it.

## 11. Fracture

FractureIndex is supplied by TB-009. TB-019 does not independently detect fracture. Rows after the applicable fracture boundary are excluded from the valid engineering curve by the relevant Method rule, while remaining in Raw Dataset.

## 12. Rm vs Fracture

RmIndex and FractureIndex are distinct concepts and are not assumed equal unless the Method/Event Engine explicitly establishes that relationship.

## 13. Valid Region

```text
ValidRegion
= StartBoundary + EndBoundary + EligibilityRules
```

The Method-specific ValidRegion controls which rows are eligible for standard calculations.

## 14. Eligibility Status

Rows may be classified as:

```text
VALID
INVALID_STRESS
INVALID_STRAIN
INVALID_SOURCE
OUTSIDE_TEST_REGION
POST_FRACTURE
GAP
DUPLICATE
```

Eligibility status never means deletion of the Raw row.

## 15. Filtering Architecture

```text
RawDataset
    ↓
Boundary Engine
    ↓
Eligibility Engine
    ↓
ValidCurveDataset
```

## 16. No Raw Filtering

The following are prohibited on Raw Dataset:

```text
Delete
Sort
Overwrite
Re-index
```

## 17. AnalysisOrdinal

An optional AnalysisOrdinal may be assigned for internal iteration:

```text
AnalysisOrdinal = 1,2,3,...
```

but:

```text
AnalysisOrdinal ≠ DatasetIndex
```

DatasetIndex remains the permanent traceability key.

## 18. Array Alignment

The following arrays must remain aligned:

```text
ValidDatasetIndex()
ValidStress()
ValidStrain()
ValidTime()
ValidForce()
ValidSource()
ValidSegment()
```

For every analytical ordinal, all values refer to the same DatasetIndex.

## 19. Order Preservation

Valid Dataset points retain original file order. No sorting by Stress, Strain, Force or Time is performed by TB-019.

## 20. Engineering Curve

The Method engineering curve is:

```text
X = EngineeringStrain
Y = EngineeringStress
```

Stress comes from TB-017 and Strain from TB-018. TB-019 does not recalculate either quantity.

## 21. Graph Correction Separation

Calculation Curve Dataset and Graph Curve Dataset are independent:

```text
CalculationCurveDataset
GraphCurveDataset
```

Without graph correction, the two may be identical. Graph-only strain correction never overwrites Calculation Strain.

## 22. ISO 6892-1 Method Input

The ISO 6892-1 Method Engine consumes `ValidCurveDataset`, not Raw Dataset.

## 23. Rp0.2

TB-008 consumes the validated Stress/Strain Curve Dataset. Pre-test and post-fracture points are not included unless a Method rule explicitly requires them.

## 24. Young's Modulus

TB-011 selects the elastic region from the Valid Dataset. Initial/preload boundaries must already be resolved before elastic-region selection.

## 25. Rm

Rm is obtained from the valid Engineering Stress Dataset subject to TB-009 boundaries and Method rules.

## 26. Yield Detection

TB-006 defines yield detection methodology. TB-019 supplies the validated source-aware curve and does not implement yield detection itself.

## 27. Extensometer Transition

TB-018 determines source segmentation. TB-019 preserves it without changing source states.

Example:

```text
CROSSHEAD
CROSSHEAD
EXTENSOMETER
EXTENSOMETER
CROSSHEAD
CROSSHEAD
```

remains exactly source-segmented in the analysis dataset.

## 28. Event Boundaries

Events retain:

```text
EventType
DatasetIndex
Time
SourceBefore
SourceAfter
Status
```

Event records remain independently auditable.

## 29. Boundary Validation

If:

```text
TestStartIndex >= FractureIndex
```

when both are required by the Method, the boundary configuration is invalid rather than silently corrected.

## 30. Missing Boundaries

If a required boundary is missing, the engine must report the missing-boundary condition. It must not invent a boundary from numeric magnitude or visual appearance.

## 31. Boundary Precedence

The logical pipeline is:

```text
Raw Dataset
    ↓
Test Start
    ↓
Method Eligibility
    ↓
Terminal Boundary
    ↓
Fracture/Post-Fracture Rule
```

Method-specific precedence is explicit configuration, not an implicit algorithm.

## 32. Duplicate DatasetIndex

Duplicate DatasetIndex values are flagged. TB-019 does not silently delete one duplicate.

## 33. Missing DatasetIndex

A row without a valid DatasetIndex cannot become a ValidCurveDataset point.

## 34. Time Integrity

Duplicate timestamps are not automatically invalid because multiple measurements may share a timestamp. DatasetIndex remains the primary key.

Non-monotonic Time is flagged but Raw data is not sorted.

## 35. Displacement/Strain Monotonicity

Non-monotonic Displacement or Strain is not, by itself, a reason to delete a row. It may represent unloading, machine compliance, transition behavior or post-fracture movement and must be interpreted by the relevant Method/Analysis layer.

## 36. Gaps

If:

```text
DatasetIndex(i+1) > DatasetIndex(i) + 1
```

a gap may exist and is flagged. TB-019 does not automatically interpolate the gap.

## 37. Outliers

Outliers are flagged, not deleted. Outlier treatment belongs to the appropriate Analysis/Method layer.

## 38. Curve Continuity

TB-019 may report continuity issues but does not alter points merely to make a curve visually smoother.

## 39. No Smoothing

Automatic smoothing is prohibited in TB-019.

## 40. No Resampling

TB-019 does not resample the original measurement series.

## 41. No Interpolation

Interpolation is prohibited unless explicitly authorized by the applicable Method.

## 42. No Extrapolation

No points outside the original Dataset may be generated by TB-019.

## 43. Point Counts

The analysis session records:

```text
RawPointCount
ValidPointCount
InvalidPointCount
ExcludedPointCount
```

## 44. Exclusion Reason

Every excluded analysis point should have an auditable reason, for example:

```text
PRE_TEST
POST_FRACTURE
INVALID_STRESS
INVALID_STRAIN
INVALID_SOURCE
DUPLICATE
GAP
OUTSIDE_METHOD_REGION
```

## 45. Audit Trail

Each filtering/analysis session records:

```text
AnalysisVersion
Method
StartBoundary
EndBoundary
ExcludedCount
Rules
Timestamp
```

## 46. Recalculation

Changes to parameters affecting the Valid Curve, including L0, Area0, Source Event, Reference, TestStart or Fracture Boundary, trigger rebuilding of the Derived ValidCurveDataset.

## 47. Dependency Chain

```text
Raw TXT
 ↓
Dataset
 ↓
Events
 ↓
Stress
 ↓
Strain
 ↓
Boundaries
 ↓
ValidCurveDataset
 ↓
ISO 6892-1 Method
```

## 48. Dependency Direction

TB-019 must not depend on final results such as Rp0.2, Rm or Young's Modulus to determine which rows are valid. This prevents circular dependencies.

## 49. Versioning

The following versions remain distinct:

```text
RawDataVersion
CalculationVersion
AnalysisVersion
MethodVersion
```

## 50. Traceability

A result remains reconstructable:

```text
Rp0.2
 ↓
CurvePoint
 ↓
DatasetIndex
 ↓
Stress / Strain
 ↓
Source / SegmentID
 ↓
Original TXT Row
```

## 51. Architecture

```text
                       RAW TXT
                          │
                          ▼
                   Dataset Builder
                          │
                          ▼
                 Event / Boundary Engine
                          │
             ┌────────────┴────────────┐
             ▼                         ▼
        TB-017 Stress             TB-018 Strain
             │                         │
             └────────────┬────────────┘
                          ▼
                   Pairing Engine
                          │
                          ▼
                   Validity Engine
                          │
                          ▼
                 ValidCurveDataset
                          │
                          ▼
                 ISO 6892-1 Engine
```

## 52. Freeze Decisions

| ID | Decision |
|---|---|
| D-341 | Raw Dataset is Immutable. |
| D-342 | Stress and Strain are paired only by shared DatasetIndex. |
| D-343 | CurvePoint is a single Stress/Strain/Index entity. |
| D-344 | Missing Stress or Strain makes the CurvePoint invalid for Method calculation. |
| D-345 | Missing is not equivalent to Zero. |
| D-346 | TestStart Boundary is supplied by TB-015. |
| D-347 | Fracture Boundary is supplied by TB-009. |
| D-348 | TB-019 does not independently detect Fracture. |
| D-349 | RmIndex and FractureIndex are not assumed identical. |
| D-350 | ValidCurveDataset is a Derived Dataset. |
| D-351 | Filtering never deletes Raw Rows. |
| D-352 | DatasetIndex is preserved after Filtering. |
| D-353 | AnalysisOrdinal, when used, is distinct from DatasetIndex. |
| D-354 | No independent Stress/Strain sorting or re-indexing is permitted. |
| D-355 | Source Segmentation is supplied by TB-018 and is not changed by TB-019. |
| D-356 | Gaps are not automatically interpolated. |
| D-357 | Outliers are not deleted by TB-019. |
| D-358 | Non-monotonic Displacement/Strain alone does not invalidate a row. |
| D-359 | Non-monotonic Time is flagged and Raw data is not sorted. |
| D-360 | Duplicate DatasetIndex is flagged without automatic deletion. |
| D-361 | Resampling is not performed by TB-019. |
| D-362 | Extrapolation is not performed by TB-019. |
| D-363 | Automatic smoothing is prohibited. |
| D-364 | Point counts and exclusion reasons are recorded. |
| D-365 | ValidCurveDataset is rebuilt when relevant boundaries or calculation parameters change. |
| D-366 | Method Engine consumes ValidCurveDataset rather than Raw Dataset. |
| D-367 | Circular dependency between Results and Valid Dataset is prohibited. |
| D-368 | Calculation, Analysis and Method versions remain distinct. |
| D-369 | Curve points remain traceable to the original TXT row. |
| D-370 | All processing remains Array-Based and DatasetIndex-aligned. |

## 53. Status

**Approved / Frozen — TB-019.**
