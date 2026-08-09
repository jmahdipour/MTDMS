# TB-026 — ISO 6892-1 Test Package Lifecycle, State Machine & Finalization Rules Specification

**Status:** Approved / Frozen  
**Parent:** TB-025  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in

## 1. Purpose

Defines the lifecycle of a Test Result Package from TXT import through normalization, calculation, review, validation, finalization, correction, recalculation and superseding.

## 2. Official States

```text
IMPORTED
NORMALIZED
CALCULATED
REVIEW_REQUIRED
CORRECTED
RECALCULATED
VALIDATED
FINALIZED
SUPERSEDED
FAILED
INCOMPLETE
```

## 3. Normal Lifecycle

```text
IMPORTED
   ↓
NORMALIZED
   ↓
CALCULATED
   ↓
VALIDATED
   ↓
FINALIZED
```

Correction path:

```text
VALIDATED → REVIEW_REQUIRED → CORRECTED → RECALCULATED → VALIDATED
```

Versioning path:

```text
FINALIZED V1 → SUPERSEDED V1
                    ↑
              FINALIZED V2
```

Critical failure may move a package to `FAILED`; missing mandatory information may move it to `INCOMPLETE`.

## 4. IMPORTED

Source TXT has been successfully read and a RawDataset has been created.

Required conditions:

- Source identity recorded.
- File integrity available.
- Raw data imported.
- OriginalRowIndex preserved.

Finalization is prohibited.

## 5. NORMALIZED

Units, columns and formats required for analysis have been normalized. Original units and conversion provenance remain traceable.

## 6. CALCULATED

Required analytical quantities have been calculated, as applicable:

```text
Stress
Strain
YoungModulus
Yield
Rp0.2
Rm
Fracture
A%
TrueStress
TrueStrain
```

A numeric Result is not automatically a valid Result.

## 7. REVIEW_REQUIRED

Used when analytical output requires operator review, including ambiguous:

- Yield detection
- Rp0.2 region
- Fracture detection
- Extensometer Release
- Elastic-region selection
- Graph correction

## 8. CORRECTED

An operator has changed an analytical boundary, Event or correction parameter. Raw data is never overwritten.

Automatic and operator values are both retained.

## 9. RECALCULATED

All Results affected by a changed dependency are recalculated and assigned to the new Package Version.

Example:

```text
ExtensometerRelease changed
        ↓
EngineeringStrain
YoungModulus
Rp0.2
A%
```

## 10. VALIDATED

The package has passed required structural, dataset, event, calculation, Result, provenance and audit validation, with no blocking Critical Error.

Warnings may remain where the approved validation rules permit them.

## 11. FINALIZED

Finalization means the Package is approved for release of analytical Results and Report.

Required gates:

```text
Source Validation
        ↓
Dataset Validation
        ↓
Event Validation
        ↓
Calculation Validation
        ↓
Result Validation
        ↓
Provenance Validation
        ↓
Audit Validation
        ↓
Integrity Check
        ↓
FINALIZED
```

## 12. Finalization Conditions

A Package cannot be Finalized when:

- Source is invalid.
- Required Dataset is incomplete.
- Critical Event is unresolved.
- Required calculation failed.
- Provenance is broken.
- Audit is not persisted.
- Package integrity fails.
- Required operator review remains unresolved.

## 13. Event Finalization

The following Events must be resolved according to their applicability:

```text
TestStart
ExtensometerRelease
Yield
Rp0.2
Rm
Fracture
```

Event statuses include:

```text
AUTO_ACCEPTED
OPERATOR_ACCEPTED
OPERATOR_OVERRIDDEN
AMBIGUOUS
INVALID
```

Critical unresolved Events block Finalization.

## 14. Extensometer Release

`ExtensometerRelease` remains independent from Yield, Rp0.2 and Fracture.

The final strain source segmentation must be known before Finalization:

```text
0 → ExtensometerRelease     Extensometer
ExtensometerRelease → End   Crosshead
```

Any operator override is auditable and versioned.

## 15. Fracture

Fracture remains an independent Event and defines the boundary required for post-fracture handling.

After Finalization its effective index is immutable within that Package Version. A later change creates a new Version.

## 16. Rp0.2

Rp0.2 depends on its approved stress/strain Dataset, reference Young's Modulus, offset, valid search region and Method Version. Any dependency change requires recalculation.

## 17. Graph Correction

Graph Correction is separated from Raw Data:

```text
Raw Strain
    ↓
Correction Parameters
    ↓
Corrected Strain / Presentation Curve
```

Correction parameters must be resolved before Finalization if the corrected graph is part of the released result package.

## 18. Secondary Gauge Length

Operator-provided post-fracture secondary gauge length may affect:

```text
A%
Horizontal Axis Correction
```

Changing it therefore creates a new Package Version and triggers the affected recalculations.

## 19. Finalized Package Immutability

A Finalized Package Version is not edited in place.

Correct workflow:

```text
FINALIZED V1
      ↓
Create V2
      ↓
Modify / Correct
      ↓
Recalculate
      ↓
Validate
      ↓
FINALIZED V2
```

## 20. SUPERSEDED

When a newer version is finalized, the previous finalized version becomes `SUPERSEDED` but remains persisted and auditable.

## 21. FAILED

Used for a package that contains a critical analytical or integrity failure, such as corrupted source data, corrupted Dataset, calculation failure or integrity failure.

`FAILED` cannot transition directly to `FINALIZED`.

## 22. INCOMPLETE

Used when required information has not yet been supplied or processing is unfinished. It is distinct from `FAILED`.

## 23. Forbidden Direct Transitions

The following are prohibited:

```text
IMPORTED    → FINALIZED
NORMALIZED  → FINALIZED
CALCULATED  → FINALIZED
FAILED      → FINALIZED
INCOMPLETE  → FINALIZED
```

A package must pass the required intermediate gates.

## 24. Recalculation Rule

Any change to a Result dependency invalidates the affected Finalized calculation and requires a new version.

Examples:

```text
ExtensometerRelease
L_after
Rp0.2 Offset
YoungModulus Reference
Elastic Region
Fracture Index
```

## 25. Material Library Changes

Changes to the current Material Library do not modify historical packages. The package uses its stored Material Snapshot.

## 26. Configuration Changes

Changes to application Settings do not modify historical packages. The effective test-time Configuration Snapshot remains authoritative for the historical version.

## 27. Operator Override

An override retains:

```text
AutomaticValue
OperatorValue
FinalValue
Operator
Timestamp
Reason
```

The automatic result is never silently destroyed.

## 28. Report Release

Final Report generation is permitted only from a `FINALIZED` Package Version.

Packages in `CALCULATED`, `REVIEW_REQUIRED`, `FAILED` or `INCOMPLETE` states are not releasable as Final Reports.

## 29. Release State vs Calculation State

The following are independent concepts:

```text
Calculation State
Validation State
Release State
```

For example, calculations can be complete while the package remains unreleased because operator review is pending.

## 30. MVP States

The MVP implements:

```text
IMPORTED
NORMALIZED
CALCULATED
REVIEW_REQUIRED
CORRECTED
RECALCULATED
VALIDATED
FINALIZED
SUPERSEDED
FAILED
INCOMPLETE
```

## 31. Scope Exclusions

TB-026 does not define:

- PLC communication
- Machine control
- Real-time acquisition
- Online device integration
- LIMS integration
- Cloud synchronization
- Distributed storage
- Multi-user concurrency

All lifecycle rules apply exclusively to the TXT output analysis Package.

## 32. Freeze Decisions

| ID | Decision |
|---|---|
| D-546 | Package has a formal State Machine. |
| D-547 | Finalization requires all approved Finalization Gates. |
| D-548 | RawDataset is immutable throughout the lifecycle. |
| D-549 | Corrections create a new Package Version. |
| D-550 | Recalculation creates a new Package Version. |
| D-551 | Finalized versions are not edited in place. |
| D-552 | Previous versions are retained. |
| D-553 | Previous Finalized versions become SUPERSEDED when a newer version is finalized. |
| D-554 | FAILED Packages cannot be Finalized. |
| D-555 | INCOMPLETE and FAILED are distinct states. |
| D-556 | ExtensometerRelease and Fracture remain independent Events. |
| D-557 | Changes to critical Event dependencies trigger affected recalculation. |
| D-558 | L_after may affect A% and horizontal-axis correction and therefore requires versioned recalculation. |
| D-559 | Material Library changes do not modify historical Results. |
| D-560 | Historical Configuration is preserved as a Package Snapshot. |
| D-561 | Operator Override never deletes the automatic value. |
| D-562 | Final Reports are released only from FINALIZED Packages. |
| D-563 | Calculation, Validation and Release states are independent concepts. |
| D-564 | The lifecycle is exclusively for exported TXT file analysis. |

**Status: Approved / Frozen — TB-026.**
