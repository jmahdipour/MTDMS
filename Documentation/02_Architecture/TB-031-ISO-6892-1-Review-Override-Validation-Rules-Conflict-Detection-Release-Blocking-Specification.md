# TB-031 — ISO 6892-1 Review/Override Validation Rules, Conflict Detection & Release Blocking Specification

**Status:** Approved / Frozen  
**Parent:** TB-030  
**Scope:** Exported TXT tensile-test file analysis only  
**Platform:** Excel 2019 VBA Add-in

## 1. Purpose

Defines validation rules for Automatic Analysis and Operator Overrides, conflict detection, consistency checks, provenance checks and the Final Release Gate.

**Core rule:** An Operator Override is not valid merely because it was entered by an Operator. It must remain consistent with the Dataset, Events, Boundaries, active Methodology, Dependencies and Results.

## 2. Validation Architecture

```text
Automatic Analysis / Operator Override
                 ↓
          Override Validation
                 ↓
        Conflict Detection
                 ↓
       Dependency Validation
                 ↓
       ISO Method Validation
                 ↓
        Result Consistency
                 ↓
        Release Gate Status
```

## 3. Validation Levels

```text
LEVEL 0 — Data Integrity
LEVEL 1 — Event / Boundary Integrity
LEVEL 2 — Calculation Consistency
LEVEL 3 — Release Eligibility
```

## 4. Level 0 — Data Integrity

Validate:

```text
Index exists
Index within Dataset
Numeric value valid
Unit valid
Timestamp valid
Required field present
Source Dataset available
```

An index outside the available Dataset is `CRITICAL`.

## 5. Level 1 — Event / Boundary Integrity

Required ordering includes:

```text
TestStart < ExtensometerRelease
TestStart < Yield
TestStart < Rp0.2
TestStart < Rm
TestStart < Fracture
```

Where applicable:

```text
RmIndex < FractureIndex
```

## 6. Independent Event Rule

The following remain independent Events:

```text
ExtensometerRelease
Yield
Rm
Fracture
```

Validation reports conflicts but does not silently move one Event because another Event changed.

## 7. Extensometer Release Validation

```text
TestStart < ReleaseIndex < DatasetEnd
```

After Release:

```text
0 → ReleaseIndex       = EXTENSOMETER
ReleaseIndex → End     = CROSSHEAD
```

The transition must be reflected in the Strain Source layer.

## 8. Yield Validation

Unless the active Methodology defines another valid boundary:

```text
TestStart < YieldIndex < RmIndex
```

A Yield boundary outside the permitted region is `CRITICAL`.

## 9. Rp0.2 Validation

```text
TestStart < Rp02Index < FractureIndex
```

The Rp0.2 point must also satisfy the active Rp0.2 search-region and methodology rules.

## 10. Elastic Region Validation

```text
TestStart <= ElasticStartIndex
ElasticStartIndex < ElasticEndIndex
ElasticEndIndex <= YieldIndex
```

If the active Methodology defines a different relationship, the Methodology RuleSet takes precedence.

## 11. Young's Modulus Validation

Young's Modulus must:

- originate from a valid Elastic Region or approved Material Library source;
- have valid units;
- be finite;
- not be NaN or Infinity;
- reference a valid calculation region.

## 12. Rm Validation

Rm must be consistent with the active Methodology and valid Dataset:

```text
RmIndex ∈ ValidDataset
Stress[RmIndex] = Rm
```

## 13. Rm / Fracture Conflict

Default rule:

```text
RmIndex < FractureIndex
```

Violation produces a `CRITICAL` blocking Conflict unless the active Methodology explicitly defines another permitted condition.

## 14. Fracture Validation

```text
TestStart < FractureIndex <= DatasetEnd
```

Post-fracture data must not precede the Fracture boundary.

## 15. Secondary Gauge Length Validation

For `L0` and `L_after`:

```text
L0 > 0
L_after > 0
```

and the result must be calculable:

```text
A% = (L_after - L0) / L0 × 100
```

Non-positive mandatory gauge lengths are `CRITICAL`.

## 16. Negative Elongation

If:

```text
L_after < L0
```

the system does not silently correct the value. It creates a Warning or Critical issue according to the active Methodology/Release RuleSet.

## 17. Horizontal Axis Correction Validation

Graph correction must preserve Raw Strain:

```text
RawStrain unchanged
```

Corrected Strain is stored only in the analytical/presentation layer.

## 18. Material Library Validation

If graph correction uses Material Library data:

```text
MaterialID valid
YoungModulus valid
```

Missing mandatory Material Library data results in `REVIEW_REQUIRED` and may become `BLOCKING` according to the active Release RuleSet.

## 19. Override Conflict Detection

Two or more Overrides are conflicting when their combined final state violates an active Rule.

Example:

```text
Rm = 1600
Fracture = 1541
```

violates:

```text
RmIndex < FractureIndex
```

and creates a blocking Conflict.

## 20. Conflict Object

```text
ConflictID
ReviewSessionID
OverrideID_A
OverrideID_B
RuleID
ObjectType_A
ObjectType_B
Severity
Message
ResolutionStatus
```

## 21. Conflict Status

```text
OPEN
RESOLVED
ACCEPTED_WITH_WARNING
BLOCKING
CANCELLED
```

## 22. Automatic vs Operator Difference

A difference between automatic and operator values is not itself an Error.

Example:

```text
Automatic Fracture = 1532
Operator Fracture  = 1541
```

If the Operator value passes validation, the Override is valid.

## 23. Dataset Conflict

An Override that points to a Dataset location inconsistent with the actual test data produces `REVIEW_REQUIRED` or `BLOCKING`, depending on the RuleSet.

## 24. Strain Source Conflict

An Override that assigns a Strain Source inconsistent with the Extensometer/Crosshead boundary is a `SOURCE_CONFLICT`.

Example:

```text
ExtensometerRelease = 862
Strain Override at 850 = CROSSHEAD
```

## 25. Raw Dataset Modification Prohibition

An Override may not directly modify:

```text
Force[i]
Strain[i]
Time[i]
Displacement[i]
Raw TXT data
```

Such an operation is `CRITICAL` and `BLOCKING`.

## 26. Calculation Dependency Conflict

If an Override is valid but required Results remain dirty:

```text
Override = VALID
Result = DIRTY
```

Release is `BLOCKED` until Recalculation and Validation are complete.

## 27. Validation Rule Object

```text
RuleID
RuleVersion
RuleType
Severity
Blocking
Description
```

Severity and Blocking are separate properties.

## 28. Rule Categories

```text
DATA_INTEGRITY
EVENT_ORDER
BOUNDARY
SOURCE_SEGMENTATION
CALCULATION
UNIT
METHOD
RESULT_CONSISTENCY
PROVENANCE
OVERRIDE
RELEASE
```

## 29. Severity

```text
INFO
WARNING
CRITICAL
```

`INFO` does not block Release. `WARNING` may require Review. `CRITICAL` normally blocks Release unless explicitly configured otherwise by the active RuleSet.

## 30. Package Validation State

```text
VALIDATION_PENDING
VALID
VALID_WITH_WARNING
INVALID
BLOCKED
```

## 31. Validation State Transition

```text
VALIDATION_PENDING
       ↓
   Validation
       ↓
 ┌─────┼────────┐
 ↓     ↓        ↓
VALID WARNING  INVALID
        ↓
VALID_WITH_WARNING
```

## 32. Release Blocking Conditions

Final Release is blocked when any mandatory condition is present:

```text
CRITICAL Validation Issue
OPEN Blocking Conflict
DIRTY Required Node
INVALID Required Node
BLOCKED Required Node
Pending Recalculation
Pending Validation
Missing Mandatory Measurement
Missing Mandatory Provenance
```

## 33. Release Eligibility

```text
ReleaseEligible =
    NoBlockingValidationIssue
AND NoBlockingConflict
AND NoDirtyRequiredNode
AND NoInvalidRequiredNode
AND NoPendingCalculation
AND NoPendingValidation
AND MandatoryInputsComplete
AND ProvenanceComplete
```

## 34. REVIEW_REQUIRED vs BLOCKED

These states are distinct.

Example:

```text
Low Automatic Detection Confidence
        ↓
REVIEW_REQUIRED
```

whereas:

```text
RmIndex >= FractureIndex
        ↓
BLOCKED
```

## 35. Operator Conflict Resolution

```text
Conflict
 ↓
Operator Review
 ↓
Modify Override
OR
Cancel Override
OR
Accept Warning
 ↓
Recalculate
 ↓
Validate
```

Blocking Conflicts cannot be resolved by acknowledgement alone.

## 36. Non-Blocking Warning Acceptance

A non-blocking Warning may be accepted only with documented Operator reason:

```text
Warning
 ↓
Operator Reason
 ↓
ACCEPTED_WITH_WARNING
```

## 37. Override Cancellation

Incorrect Overrides are retained but transitioned to:

```text
CANCELLED
```

After cancellation:

```text
Rebuild Impact Set
 ↓
Recalculate
 ↓
Validate
```

## 38. Batch Validation

Multiple Overrides are validated against their **combined final analytical state**, not independently only.

```text
Multiple Overrides
 ↓
Impact Union
 ↓
Single Recalculation
 ↓
Complete Validation
```

## 39. Validation Order

```text
1. Data Integrity
2. Override Integrity
3. Event Ordering
4. Boundary Integrity
5. Source Segmentation
6. Calculation Completeness
7. Result Consistency
8. Provenance
9. Release Gate
```

## 40. Validation Completeness

A Validation Run is complete only when:

```text
ExecutedRules = RequiredRules
```

If not:

```text
VALIDATION_PENDING
```

## 41. Rule Versioning

Every Validation Run records the active `ValidationVersion` / RuleSet version so the result remains reproducible.

## 42. Methodology Dependency

Method-dependent Rules are supplied by the active Methodology RuleSet rather than being duplicated as uncontrolled hard-coded rules.

```text
Standard
 ↓
Method
 ↓
RuleSet
 ↓
Validation
```

Example:

```text
ISO 6892-1
 ↓
Rp0.2 Method
 ↓
RP02-RULESET-v1
```

## 43. Provenance Validation

A Final Result must be traceable to:

```text
Source TXT
RawDataset
Analysis Version
Calculation Run
Validation Run
Review Session
Operator Override, where applicable
```

Missing mandatory provenance is `CRITICAL` and `BLOCKING`.

## 44. Audit Validation

Every accepted Override must have its corresponding Audit record.

```text
Override exists
AND
Audit exists
```

If not:

```text
CRITICAL
BLOCKED
```

## 45. Snapshot Validation

A Review Snapshot may be created only when:

```text
ReviewSession = COMPLETED
Validation = PASS / PASS_WITH_WARNING
No Blocking Issue
```

## 46. Final Package Validation

Before Finalization:

```text
Raw Dataset = IMMUTABLE
Analysis = COMPLETE
Overrides = RESOLVED
Dependencies = CLEAN
Validation = COMPLETE
Conflicts = RESOLVED
Provenance = COMPLETE
Release Gate = OPEN
```

## 47. Complete Example

```text
Automatic Analysis
       ↓
Fracture = 1532
ExtRelease = 840
       ↓
Operator Review
       ↓
Fracture → 1541
ExtRelease → 862
L_after → 65.4
       ↓
Impact Propagation
       ↓
Recalculate
       ↓
Validation
       │
       ├── Event Order       PASS
       ├── Strain Source     PASS
       ├── Rm < Fracture     PASS
       ├── L_after           PASS
       ├── Provenance        PASS
       └── Audit             PASS
       ↓
Release Gate
       ↓
OPEN
       ↓
Finalize
```

## 48. Blocking Conflict Example

```text
Operator:
Rm = 1600
Fracture = 1541
```

Validation:

```text
VAL-RM-001
RmIndex < FractureIndex
```

Result:

```text
CRITICAL
BLOCKING
Release Gate = CLOSED
```

The Operator must correct or cancel one of the conflicting Overrides.

## 49. Final Release Gate

```text
                  ┌─────────────────┐
                  │ Validation Run  │
                  └────────┬────────┘
                           ↓
                ┌────────────────────┐
                │ Blocking Issues ?  │
                └──────┬───────┬─────┘
                       │YES    │NO
                       ↓       ↓
                    BLOCKED   Continue
                               ↓
                     ┌─────────────────┐
                     │ Dirty Nodes ?   │
                     └──────┬────┬─────┘
                            │YES │NO
                            ↓    ↓
                         BLOCKED Continue
                                  ↓
                         ┌────────────────┐
                         │ Provenance OK? │
                         └──────┬────┬────┘
                                │NO  │YES
                                ↓    ↓
                             BLOCKED OPEN
```

## 50. MVP Validation Rules

```text
VAL-DATA-001  Index range
VAL-DATA-002  Numeric validity
VAL-EVT-001   TestStart ordering
VAL-EVT-002   ExtensometerRelease ordering
VAL-EVT-003   Rm before Fracture
VAL-EVT-004   Fracture boundary
VAL-STR-001   Strain source segmentation
VAL-EL-001    Elastic region validity
VAL-RM-001    Rm consistency
VAL-FR-001    Fracture consistency
VAL-GL-001    Gauge length validity
VAL-GR-001    Graph correction integrity
VAL-AUD-001   Audit existence
VAL-PROV-001  Provenance completeness
VAL-REL-001   Release gate
```

## 51. Freeze Decisions

| ID | Decision |
|---|---|
| D-647 | Every Override must pass Validation before Acceptance. |
| D-648 | Automatic/Operator difference is not itself an Error. |
| D-649 | Independent Events remain independent. |
| D-650 | Rm must precede Fracture unless an approved Methodology explicitly defines otherwise. |
| D-651 | Invalid Dataset indexes are CRITICAL. |
| D-652 | Raw Dataset modification through Override is prohibited. |
| D-653 | Calculation and Validation dependencies are separate concepts. |
| D-654 | Dirty Required Nodes block Release. |
| D-655 | Invalid Required Nodes block Release. |
| D-656 | Pending Recalculation blocks Release. |
| D-657 | Pending Validation blocks Release. |
| D-658 | Blocking Conflicts cannot be accepted merely by Operator acknowledgement. |
| D-659 | Non-blocking Warnings may be accepted with documented reason. |
| D-660 | Multiple Overrides are validated against the combined final analytical state. |
| D-661 | Validation is performed after Batch Recalculation. |
| D-662 | Every Validation Run records its Rule Version. |
| D-663 | Methodology-dependent Rules come from the active RuleSet. |
| D-664 | Missing mandatory Provenance blocks Release. |
| D-665 | Override without corresponding Audit is invalid. |
| D-666 | Review Snapshot requires completed Review and successful Validation. |
| D-667 | Release Gate is the final authority before Package Finalization. |
| D-668 | All rules apply only to exported TXT-file analysis. |

**Status: Approved / Frozen — TB-031.**
