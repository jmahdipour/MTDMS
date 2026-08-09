# TB-027 — ISO 6892-1 Final Result Acceptance & Release Gate Specification

**Status:** Approved / Frozen  
**Parent:** TB-026  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in

## 1. Purpose

Defines when Results derived from an exported TXT tensile-test file may be accepted and released as Final Results.

A numeric value alone is not sufficient evidence of validity. Final release requires successful completion of the approved source, dataset, strain-source, event, calculation, method, correction, validation, provenance, audit and integrity gates.

## 2. Validation vs Acceptance

Validation answers:

> Are the data and calculations technically and structurally valid?

Acceptance answers:

> Are the validated Results acceptable for final release?

These are independent stages.

## 3. Release Gate Chain

```text
G1 Source
 ↓
G2 Dataset
 ↓
G3 Strain Source
 ↓
G4 Events
 ↓
G5 Calculations
 ↓
G6 Standard / Method
 ↓
G7 Corrections
 ↓
G8 Validation
 ↓
G9 Provenance
 ↓
G10 Audit
 ↓
G11 Integrity
 ↓
FINAL RELEASE
```

## 4. G1 — Source Gate

The TXT source must be readable, structurally supported, contain required columns/data, and have its source identity recorded.

Blocking conditions include unreadable file, missing required column, malformed dataset and unsupported source format.

## 5. G2 — Dataset Gate

Dataset integrity must be validated for Time, Force, Displacement, Strain and Stress arrays as applicable. Pairing, `DatasetIndex` and `OriginalRowIndex` must remain traceable.

## 6. G3 — Strain Source Gate

The approved source segmentation must be resolved:

```text
0 → ExtensometerRelease       Extensometer
ExtensometerRelease → End     Crosshead
```

`ExtensometerRelease` is an independent Event. An unresolved or invalid source boundary blocks dependent Results.

## 7. G4 — Event Gate

Required Events must be resolved according to the Method:

```text
TestStart
ExtensometerRelease
Yield / Rp
Rp0.2
Rm
Fracture
```

Event status values:

```text
ACCEPTED
ACCEPTED_WITH_WARNING
REVIEW_REQUIRED
REJECTED
NOT_APPLICABLE
```

Critical unresolved Events block Release.

## 8. G5 — Calculation Gate

All Method-required calculations must be completed and validated. Typical ISO 6892-1 tensile Results include:

```text
Stress
Strain
YoungModulus
Rp0.2 / Yield Result
Rm
Fracture
A%
```

True Stress/True Strain are included when enabled/required by the approved Method configuration.

## 9. Dependency Validation

A Result is acceptable only when all of its required dependencies are valid.

Example:

```text
Rp0.2
 ↓
Stress Dataset
Strain Dataset
YoungModulus
Offset
Search Region
Method Version
```

A numeric Rp0.2 with an invalid dependency is not an acceptable Result.

## 10. G6 — Standard / Method Gate

The Result must correspond to the selected standard and approved Method Version:

```text
Standard = ISO 6892-1
MethodID = approved ISO 6892-1 method
MethodVersion = recorded version
```

Method Version, Calculation Version and Configuration Version must be traceable.

## 11. G7 — Correction Gate

Corrections must have a resolved status:

```text
No Correction
Accepted Correction
Correction Pending
Correction Rejected
```

`Correction Pending` blocks Release.

Corrections never modify RawDataset.

## 12. Horizontal Axis Correction

Where enabled, horizontal-axis correction may depend on:

```text
YoungModulus
ElasticRegion
Secondary Gauge Length
Post-Fracture Elongation
```

Required correction must be completed before Release.

## 13. Secondary Gauge Length

An operator-entered post-fracture secondary gauge length must have:

- value
- unit
- provenance
- audit record
- recalculation of affected Results
- re-validation

Changing it may affect `A%` and horizontal-axis correction.

## 14. G8 — Validation Gate

Validation includes, as applicable:

```text
Structural Validation
Dataset Validation
Event Validation
Calculation Validation
Result Validation
Boundary Validation
Unit Validation
```

Severity levels:

```text
INFO
WARNING
CRITICAL
```

## 15. Warning Policy

Warnings do not automatically reject a Result. A warning may be accepted only when the approved validation rule explicitly permits it.

Each warning must be traceable through:

```text
WarningID
Description
AffectedResult
OperatorReview
Resolution
```

## 16. Critical Policy

A Critical condition causes:

```text
Acceptance = FAIL
Release = BLOCKED
```

## 17. G9 — Provenance Gate

Every Final Result must be traceable through:

```text
Final Result
 ↓
Calculation
 ↓
Derived Dataset
 ↓
Normalized Dataset
 ↓
Raw Dataset
 ↓
TXT Source Row
```

Method, Configuration, Material and Event references must also be available.

## 18. G10 — Audit Gate

Every Manual Override must have an Audit record containing at least:

```text
Operator
Timestamp
Action
Object
OldValue
NewValue
Reason
```

An unaudited correction blocks Release.

## 19. G11 — Integrity Gate

Where package hashes are maintained, the following must be verified before Release:

```text
SourceHash
DatasetHash
ResultHash
PackageHash
```

Integrity mismatch blocks Release.

## 20. Result-Level Acceptance

Acceptance is performed at both Result and Package level.

Example:

```text
Rm           = ACCEPTED
YoungModulus = ACCEPTED
Rp0.2        = REVIEW_REQUIRED
A%           = ACCEPTED
```

For MVP, Final Test Release requires all Method-required Results to be accepted or explicitly `NOT_APPLICABLE`.

## 21. Required vs Not Applicable

A required but missing Result is:

```text
MISSING_REQUIRED_RESULT
```

and blocks Release.

A Result not required by the Method is:

```text
NOT_APPLICABLE
```

and is not equivalent to zero or missing data.

## 22. Result Status

```text
FINAL
FINAL_WITH_WARNING
NOT_FINAL
INVALID
NOT_APPLICABLE
```

Only Final Results are eligible for released output.

## 23. Package Acceptance Status

```text
NOT_READY
READY_FOR_REVIEW
ACCEPTED
ACCEPTED_WITH_WARNING
REJECTED
RELEASED
SUPERSEDED
```

## 24. Acceptance Rule

```text
IF
    All Required Gates = PASS
AND All Required Results = ACCEPTED
AND No Blocking Warning
AND No Critical Error
AND Provenance Complete
AND Audit Complete
AND Integrity Valid
THEN
    ACCEPT
ELSE
    BLOCK
```

## 25. Final Release

After Acceptance:

```text
Acceptance
 ↓
Finalization
 ↓
Release
```

Release records the effective Package Version, operator and timestamp.

## 26. Release Immutability

A Released/Finalized Package Version is not edited in place. Any change creates a new Package Version.

```text
FINALIZED V1
      ↓
NEW VERSION
      ↓
CORRECT / RECALCULATE
      ↓
VALIDATE
      ↓
FINALIZED V2
```

## 27. Re-analysis

Re-analysis preserves the original Finalized Version and produces a new Version with its own calculation, validation, provenance and audit records.

## 28. Example — Normal Release

```text
TXT Imported
 ↓
Extensometer Release resolved
 ↓
Rp0.2 calculated
 ↓
Rm calculated
 ↓
Fracture detected and accepted
 ↓
Secondary Gauge Length entered
 ↓
A% recalculated
 ↓
Horizontal Axis corrected
 ↓
Validation PASS
 ↓
Audit PASS
 ↓
Integrity PASS
 ↓
ACCEPTED
 ↓
FINALIZED
 ↓
REPORT RELEASED
```

## 29. Example — Blocked Release

```text
Fracture Detection = Ambiguous
        ↓
REVIEW_REQUIRED
        ↓
Acceptance = NOT_READY
        ↓
Release = BLOCKED
```

The operator must resolve the fracture boundary before final release.

## 30. Example — Event Correction

```text
Automatic Fracture = Index 1532
Operator Fracture  = Index 1541
        ↓
Audit
        ↓
Recalculate
        ↓
Validate
        ↓
Accept
        ↓
Finalize New Version
```

## 31. Example — Extensometer Release Correction

Changing `ExtensometerRelease` requires re-evaluation of affected quantities such as:

```text
Strain
YoungModulus
Rp0.2
A%
```

The original value remains auditable.

## 32. Example — Secondary Gauge Length Correction

```text
L_after
 ↓
Post-Fracture Elongation
 ↓
A%
 ↓
Horizontal Axis Correction
```

The affected Results must be recalculated and revalidated.

## 33. Release Evidence

The released Result must answer:

> From which TXT file, Dataset, Event, Method and Configuration was this Result produced?

This is inherited from the provenance requirements of TB-024 and package requirements of TB-025.

## 34. MVP Acceptance Gate

The MVP must verify at least:

```text
✓ Source Valid
✓ Dataset Valid
✓ Strain Source Valid
✓ Required Events Resolved
✓ Required Calculations Valid
✓ ISO 6892-1 Method Valid
✓ Corrections Resolved
✓ Validation Passed
✓ Provenance Complete
✓ Audit Complete
✓ Integrity Valid
```

## 35. Scope Exclusions

This document does not define:

- PLC communication
- Machine control
- Real-time acquisition
- Online device integration
- LIMS
- Cloud release
- Electronic-signature infrastructure

All gates apply exclusively to analysis of the exported TXT file.

## 36. Freeze Decisions

| ID | Decision |
|---|---|
| D-565 | Validation and Acceptance are separate stages. |
| D-566 | Final Release requires all approved Required Gates. |
| D-567 | Acceptance is performed at Result and Package level. |
| D-568 | A missing required Result blocks Release. |
| D-569 | An invalid required Result blocks Release. |
| D-570 | Not Applicable is distinct from Missing and Zero. |
| D-571 | Warning is non-blocking only when explicitly permitted by its validation rule. |
| D-572 | Critical Error always blocks Release. |
| D-573 | ExtensometerRelease must be resolved before final Release. |
| D-574 | Fracture must be resolved before final Release. |
| D-575 | Changing L_after requires re-acceptance of affected Results. |
| D-576 | Required Horizontal Axis Correction must be resolved before Release. |
| D-577 | Manual Override without Audit blocks Release. |
| D-578 | Incomplete Provenance blocks Release. |
| D-579 | Integrity Failure blocks Release. |
| D-580 | Released/Finalized versions are not edited in place. |
| D-581 | Re-analysis creates a new Version. |
| D-582 | Final Report is generated only from an accepted/finalized Package. |
| D-583 | Release Gates apply only to exported TXT file analysis. |

**Status: Approved / Frozen — TB-027.**
