# TB-021 — ISO 6892-1 Fracture Event Finalization, Post-Fracture Dataset & Elongation Measurement Boundary Specification

**Document:** TB-021  
**Project:** MTDMS — Material Test Data Management System  
**Version:** 1.0  
**Status:** Approved / Frozen  
**Parent:** TB-009 → TB-010 → TB-020  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in  
**Calculation model:** Array-Based

## 1. Purpose

TB-021 defines the final Fracture Event boundary and its relationship to Post-Fracture machine data and physical Elongation After Fracture measurement.

Core principle:

> Fracture Event is a Dataset boundary; Elongation After Fracture is an independent physical gauge-length measurement and must not be inferred directly from the last Stress–Strain point.

## 2. Independent Concepts

```text
Rm
 ↓
Post-Rm / Necking
 ↓
Fracture Event
 ↓
Post-Fracture Machine Data
 ↓
Physical Gauge-Length Measurement
 ↓
Elongation After Fracture
```

These concepts remain separate.

## 3. Fracture Event

A FractureEvent contains at least:

```text
FractureEvent
├── DatasetIndex
├── Time
├── Force
├── Stress
├── Strain
├── StrainSource
├── SegmentID
└── DetectionMethod
```

## 4. FractureIndex

`FractureIndex` is the DatasetIndex of the finalized fracture point:

```text
FractureIndex = DatasetIndex
```

## 5. Fracture Is Not Last TXT Row

`LastTXTDataRow` is not automatically `FractureIndex`. The file may contain additional measurements after physical fracture.

## 6. Fracture Is Not Zero Force

`Force = 0` is not, by itself, a fracture rule.

## 7. Fracture Is Not Minimum Force

Minimum Force is not, by itself, a fracture rule.

## 8. Detection and Finalization

TB-009 determines the detection methodology. TB-021 performs validation and finalization:

```text
CandidateFractureIndex
        ↓
Validation
        ↓
FinalFractureIndex
```

## 9. Multiple Candidates

If multiple candidates exist, the system may retain a `FractureCandidate[]` collection and a `FractureConfidence` value. Exactly one final boundary must be selected for the finalized test analysis.

## 10. Detection Method

The final event records the detection method, such as:

```text
FORCE_DROP
STRESS_DROP
EXTENSOMETER_SIGNAL
OPERATOR_MARKER
METHOD_SPECIFIC
```

## 11. Operator Override

Operator correction is allowed in the Graph Analysis layer when supported by the workflow. The system must preserve:

```text
AutomaticFractureIndex
OperatorFractureIndex
FinalFractureIndex
```

and must never silently replace the automatic decision.

## 12. Raw Data Preservation

Changing the fracture boundary never modifies the original TXT-derived Dataset.

## 13. Post-Fracture Dataset

By default:

```text
DatasetIndex > FinalFractureIndex
```

is flagged as `PostFracture`.

The fracture point itself remains in the Dataset.

## 14. Post-Fracture Tail

The rows after the final fracture boundary form the `PostFractureTail` and remain preserved and traceable for audit and data-quality analysis.

## 15. Boundary Separation

The system maintains three distinct boundaries:

```text
RmIndex
FinalFractureIndex
LastDatasetIndex
```

For example:

```text
RmIndex       = 1500
FractureIndex = 1740
LastDataset   = 1755
```

is valid.

## 16. Curve Terminal Boundary

The engineering curve terminal boundary is explicit. It may equal FinalFractureIndex when the applicable Method specifies this, but the equality is not assumed implicitly.

## 17. Post-Fracture Data for Audit

Post-fracture machine rows remain available for:

- device behavior review
- fracture-event verification
- data-registration delay analysis
- Crosshead behavior review
- audit trail

## 18. Physical Gauge-Length Measurement

After fracture, physical gauge length is represented separately as:

```text
L_after
```

It is not a Curve Dataset point.

## 19. Original Gauge Length

The original gauge length is:

```text
L0
```

and is supplied by the sample/test definition.

## 20. Elongation After Fracture

Where the applicable standard/reporting method defines the result in this form:

```text
A% = ((L_after - L0) / L0) × 100
```

The result is based on physical post-fracture gauge-length measurement, not merely the last Engineering Strain value.

## 21. Measurement Source

`L_after` records its source, for example:

```text
OPERATOR
CALIPER
GAUGE_MEASUREMENT
MANUAL_INPUT
```

## 22. Manual Measurement Record

A manual measurement record contains, where applicable:

```text
L0
L_after
Unit
MeasurementDate
Operator
```

## 23. Unit Validation

`L0` and `L_after` must be normalized to a common unit before calculating elongation.

## 24. Measurement Validation

At minimum:

```text
L0 > 0
L_after > 0
```

must hold. Invalid measurements receive an explicit validation status.

## 25. Negative Elongation

If:

```text
L_after < L0
```

the software must not silently convert the result to zero. It records an explicit invalid/exception condition for operator review.

## 26. Missing L_after

If fracture is detected but `L_after` is missing:

```text
A% = NOT_AVAILABLE
```

not zero.

## 27. L_after Without Fracture

A post-fracture gauge-length measurement without a finalized Fracture Event is an inconsistent state and must be flagged for review.

## 28. Gauge-Length Measurement Boundary

`L_after` belongs to a physical measurement layer and must not be artificially mapped to a DatasetIndex.

## 29. Post-Fracture Strain

Post-fracture Engineering Strain remains available as Raw/Derived Data but is not a substitute for `L_after`.

```text
PostFractureStrain ≠ ElongationAfterFracture
```

## 30. Crosshead After Fracture

Crosshead data after fracture remains preserved and traceable. It is not a substitute for physical gauge-length measurement.

## 31. Extensometer After Fracture

Any Extensometer data after fracture is likewise preserved. Its analytical use must be Method-specific.

## 32. Extensometer Release

The approved project scenario allows:

```text
Extensometer
      ↓
Yield / Rp Region
      ↓
Release Event
      ↓
Crosshead
```

Extensometer Release and Fracture are independent Events.

## 33. Event Sequence Validation

The Event Engine validates ordering of DatasetIndex-based events. Conflicting event order is flagged rather than silently corrected.

## 34. Duplicate Fracture Events

More than one finalized Fracture Event is an error/exception condition and must be flagged.

## 35. Finalization Status

A FractureEvent may contain statuses such as:

```text
DETECTED
VALIDATED
OVERRIDDEN
CONFIRMED
REJECTED
```

## 36. Recalculation

Changing `FinalFractureIndex` rebuilds dependent Derived Datasets, but never changes Raw Dataset.

## 37. A% Recalculation

Changing only `FinalFractureIndex` does not change `L_after` or A%. A% changes when the physical measurement inputs or applicable calculation configuration changes.

## 38. Graph Correction

Changing GraphCorrectedStrain must not silently change FinalFractureIndex. Any analysis-dependent change requires explicit re-analysis according to the applicable Method.

## 39. Report Data

The reporting layer may expose:

```text
FractureIndex
FractureForce
FractureStress
FractureStrain
L0
L_after
ElongationAfterFracture
MeasurementSource
```

## 40. Traceability

The audit chain is:

```text
A%
 ↓
L_after
 ↓
Measurement Source / Operator Record
 ↓
Fracture Event
 ↓
FractureIndex
 ↓
Original TXT Dataset
```

## 41. Example

```text
RmIndex       = 1500
FractureIndex = 1740
LastDataset   = 1755
```

Therefore:

```text
1 ... 1499     Pre-Rm
1500            Rm
1501 ... 1739   Post-Rm / Necking Candidate
1740            Fracture
1741 ... 1755   Post-Fracture Tail
```

If:

```text
L0      = 50.00 mm
L_after = 62.00 mm
```

then:

```text
A% = ((62 - 50) / 50) × 100 = 24 %
```

This result is independent of the last Engineering Strain value in the TXT file.

## 42. Layer Separation

### Raw

Original TXT-derived measurements.

### Derived

Stress, Strain, Rm, Fracture, Post-Rm and Post-Fracture flags.

### Physical Measurement

`L_after` and related operator measurement metadata.

These layers must not be merged.

## 43. Prohibited Actions

TB-021 must not:

- assume the last row is fracture
- assume zero force is fracture
- assume minimum force is fracture
- delete Post-Fracture Raw rows
- infer L_after from the last strain value
- derive gauge length from the stress–strain curve
- apply Operator Override without audit data
- modify or sort Raw Dataset
- treat Post-Fracture Strain as Elongation After Fracture

## 44. Freeze Decisions

| ID | Decision |
|---|---|
| D-398 | Fracture Event is an independent Dataset boundary. |
| D-399 | FractureIndex is not necessarily the last TXT row. |
| D-400 | Zero Force alone is not Fracture. |
| D-401 | Minimum Force alone is not Fracture. |
| D-402 | Fracture Detection is defined by TB-009. |
| D-403 | TB-021 owns Fracture finalization and boundary management. |
| D-404 | CandidateFractureIndex and FinalFractureIndex are independent. |
| D-405 | Operator Override is auditable. |
| D-406 | Post-Fracture Tail is preserved in Raw Dataset. |
| D-407 | Fracture Point remains in the Dataset. |
| D-408 | RmIndex, FinalFractureIndex and LastDatasetIndex are independent. |
| D-409 | Post-Fracture Data remains available for audit. |
| D-410 | L_after is an independent physical measurement. |
| D-411 | Elongation After Fracture is calculated from L0 and L_after. |
| D-412 | Missing L_after is Not Available, not zero. |
| D-413 | L_after without a finalized Fracture Event is flagged as inconsistent. |
| D-414 | Post-Fracture Strain is not a substitute for L_after. |
| D-415 | Crosshead data after fracture is preserved. |
| D-416 | Extensometer data after fracture is preserved. |
| D-417 | Extensometer Release and Fracture are independent Events. |
| D-418 | Changing FinalFractureIndex rebuilds dependent Derived Datasets. |
| D-419 | Changing FinalFractureIndex alone does not change L_after. |
| D-420 | Graph Correction does not silently change the Raw/Final Fracture Boundary. |
| D-421 | Exactly one FinalFractureIndex is required for a finalized test. |
| D-422 | Duplicate Fracture Events are flagged. |
| D-423 | Event ordering is validated. |
| D-424 | Fracture Results remain traceable to the original TXT row. |
| D-425 | Raw, Derived and Physical Measurement layers remain independent. |

## 45. Status

**Approved / Frozen — TB-021.**
