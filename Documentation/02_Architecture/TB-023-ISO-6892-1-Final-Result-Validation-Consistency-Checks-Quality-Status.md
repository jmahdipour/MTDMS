# TB-023 — ISO 6892-1 Final Result Validation, Consistency Checks & Quality Status Specification

**Document:** TB-023  
**Project:** MTDMS — Material Test Data Management System  
**Version:** 1.0  
**Status:** Approved / Frozen  
**Parent:** TB-022  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in  
**Calculation model:** Array-Based

## 1. Purpose

TB-023 defines the final Validation layer before Results are exposed to reporting. A calculated value is not automatically a valid value; it must also satisfy data, event, boundary, dependency, consistency, traceability and applicable Method requirements.

## 2. Pipeline Position

```text
TXT
 ↓
Raw Dataset
 ↓
Normalization
 ↓
Derived Dataset
 ↓
Events / Boundaries
 ↓
Calculations
 ↓
Results
 ↓
TB-023 Validation
 ↓
Quality Status
 ↓
Final Result Package
 ↓
Report
```

## 3. Validation Is Independent

Validation does not replace Calculation. The logical flow is:

```text
Calculation Engine
        ↓
      Result
        ↓
Validation Engine
```

## 4. Validation Levels

```text
L1 — Data Validation
L2 — Event / Boundary Validation
L3 — Calculation Consistency
L4 — Final Result Validation
```

## 5. L1 — Data Validation

At minimum, validate:

```text
File Exists
File Readable
Required Columns Present
Numeric Data Valid
Units Known
Dataset Not Empty
Original Row Index Valid
```

## 6. Empty Dataset

If no valid Dataset exists:

```text
QualityStatus = INVALID
```

No final analytical Result is permitted.

## 7. Required Columns

A missing Method-required column is explicitly recorded as `RequiredColumnMissing`; it is not silently replaced with zero or another source.

## 8. Numeric Validation

Non-numeric source values must remain identifiable as invalid input. They must never be silently converted to zero.

## 9. Missing Data

Missing values are distinct from zero and receive an explicit state such as:

```text
VALID
MISSING
INVALID
```

## 10. Time Validation

Where Time is supplied:

```text
Time[i+1] >= Time[i]
```

must be checked. Non-monotonic order is flagged.

## 11. Duplicate Time

Duplicate timestamps are not automatically errors because multiple measurements can share a timestamp. They are normally a Warning unless the applicable Method prohibits them.

## 12. Original Row Integrity

Every Dataset row remains traceable to the source TXT through `OriginalRowIndex`.

## 13. L2 — Event Validation

Relevant events include:

```text
TestStart
ExtensometerRelease
Yield
Rp0.2
Rm
Fracture
```

Event order and Dataset boundaries are validated according to the applicable Method. Missing events are only errors when the Method or requested Result requires them.

## 14. Extensometer Release Validation

If present:

```text
ExtensometerReleaseIndex > TestStartIndex
```

must hold.

## 15. Fracture Validation

If present:

```text
FractureIndex >= TestStartIndex
FractureIndex <= LastDatasetIndex
```

must hold.

## 16. Fracture vs Last Dataset Row

`FractureIndex` is not required to equal `LastDatasetIndex`. A valid Post-Fracture Tail may exist.

## 17. Rm Boundary Validation

When both Events are finalized:

```text
RmIndex <= FractureIndex
```

must hold unless the applicable Method explicitly permits another state.

## 18. Rm Value Validation

For a Method defining Rm as maximum valid Engineering Stress:

```text
RmStress == Maximum Valid Engineering Stress
```

must be verified against the actual valid Dataset.

## 19. Rp0.2 Validation

Rp0.2 must use a valid Stress–Strain Dataset, valid elastic reference line, applicable offset and valid intersection. An absent valid intersection results in `NOT_AVAILABLE`, not zero.

## 20. Young's Modulus Validation

Young's Modulus must be supported by a valid elastic region and, under the applicable method, must satisfy:

```text
E > 0
```

unless a specific Method defines another valid condition.

## 21. Elastic Region Validation

Elastic Region must have valid boundaries:

```text
StartIndex < EndIndex
```

and sufficient valid data points for the applicable calculation.

## 22. Stress Validation

Cross-sectional Area must be valid and positive:

```text
Area > 0
```

If not, Stress is `INVALID`.

## 23. Stress Monotonicity

Stress is not required to be monotonic. A stress decrease alone is not an error because yielding, necking and fracture-related behavior may legitimately produce reductions.

## 24. Strain Validation

Engineering Strain must identify its source:

```text
Extensometer
Crosshead
Segmented / Combined Source
```

according to the approved source-segmentation rules.

## 25. Strain Source Boundary

Where an Extensometer Release Event exists, the actual source boundary must conform to the declared TB-005/TB-018 rule. A source change must be traceable to its Event.

## 26. Strain Continuity

A discontinuity at the Source Switch is flagged for analysis. It is not automatically classified as invalid because source Zero/Scale differences can produce a legitimate discontinuity requiring correction or operator review.

## 27. L3 — Calculation Consistency

Validation checks internal relationships between Results and their source arrays.

Examples:

```text
RmStress == Maximum Valid Stress
```

for the applicable Method.

## 28. Result Traceability

Every Result must be traceable, where applicable, to:

```text
StartIndex
EndIndex
DetectionIndex
Source
Method
```

## 29. Missing Dependency

If a required dependency is absent, the dependent Result is:

```text
NOT_AVAILABLE
```

rather than zero or a fabricated estimate.

## 30. Invalid Dependency

An `INVALID` dependency cannot produce a dependent `VALID` Result unless an explicitly declared alternative Method provides an independently valid Result.

## 31. Result Quality Status

Each Result may have:

```text
VALID
VALID_WITH_WARNING
INVALID
NOT_AVAILABLE
OVERRIDDEN
```

## 32. VALID

All required dependencies are valid, the calculation completed successfully, consistency checks passed and no disqualifying condition exists.

## 33. VALID_WITH_WARNING

The Result is usable, but one or more non-critical warnings are attached.

Examples:

```text
DuplicateTimestamp
SmallPostFractureTail
SourceSwitchJump
```

## 34. INVALID

The Result exists but its validity conditions are violated.

Example:

```text
FractureIndex < RmIndex
```

## 35. NOT_AVAILABLE

The Result cannot be produced because required data or dependency is missing or not applicable.

## 36. OVERRIDDEN

An Operator Override exists. Automatic, Operator and Final values remain separately auditable.

## 37. Validation Severity

Each validation rule has one severity:

```text
INFO
WARNING
ERROR
CRITICAL
```

## 38. INFO

Informational condition with no impact on Result validity.

Example:

```text
PostFractureTailDetected
```

## 39. WARNING

Potential data-quality or interpretation issue that does not invalidate the Result.

## 40. ERROR

The affected Result is not valid.

Example:

```text
InvalidArea
```

## 41. CRITICAL

The complete Test Package cannot be accepted as a finalized analytical result.

Examples:

```text
NoValidDataset
CorruptInput
RequiredColumnMissing
```

## 42. Test-Level Quality Status

The complete Test has:

```text
PASS
PASS_WITH_WARNING
FAIL
INCOMPLETE
```

## 43. PASS

All mandatory Results are valid and no disqualifying condition exists.

## 44. PASS_WITH_WARNING

Mandatory Results are valid but one or more non-critical Warnings exist.

## 45. FAIL

At least one Critical condition or mandatory Invalid Result prevents acceptance.

## 46. INCOMPLETE

Required information for finalization is missing.

Example:

```text
Fracture Detected
L_after Missing
```

when the requested Method/Report requires Elongation After Fracture.

## 47. Result Matrix Example

| Result | Status |
|---|---|
| Stress | VALID |
| Young Modulus | VALID |
| Rp0.2 | VALID |
| Rm | VALID |
| Fracture | VALID |
| A% | NOT_AVAILABLE |

The final Test Quality Status is determined by the Method and required-result policy, not by the presence of a single missing optional Result.

## 48. Cross-Result Consistency

Where the Events exist and the Method requires their sequence:

```text
TestStart <= Yield
TestStart <= Rm
TestStart <= Fracture
Rm <= Fracture
```

must hold.

## 49. Rm / Fracture Check

If Fracture is finalized before Rm in a Method requiring Rm first, the Test receives an inconsistency condition.

## 50. Gauge Length Validation

```text
L0 > 0
L_after > 0
```

must hold when those measurements are supplied.

After normalization:

```text
Unit(L0) == Unit(L_after)
```

must hold.

## 51. Elongation Validation

Where the normal calculation applies:

```text
L_after >= L0
```

is expected.

If:

```text
L_after < L0
```

then A% is `INVALID` and must not be silently forced to zero.

## 52. Fracture / A% Consistency

If A% is supplied or finalized without a corresponding finalized Fracture Event, an `INCONSISTENT_STATE` condition is recorded where the workflow requires the fracture boundary.

## 53. Graph Correction Validation

The Graph Correction layer validates:

```text
Raw Dataset unchanged
Correction parameters valid
Elastic reference valid
Corrected strain finite
No duplicate corrected points
```

## 54. Corrected Axis Integrity

Corrected horizontal-axis data must not contain NaN, Infinity, invalid numeric values or prohibited ordering anomalies.

## 55. Corrected Curve Boundary

Graph Correction must respect the applicable FinalFractureIndex and must not silently extend the final analytical curve into Post-Fracture data.

## 56. Material Library Validation

Where Material Library data is required:

```text
Material Exists
Property Exists
Unit Known
Value Valid
```

must be checked.

## 57. Material Library Missing

Missing Young's Modulus or another optional Material Library property makes the dependent operation `NOT_AVAILABLE`, but must not automatically invalidate independent Results such as Stress or Rm.

## 58. Operator Correction Validation

An Override record contains, where applicable:

```text
OriginalValue
NewValue
Operator
Timestamp
Reason
```

## 59. No Silent Correction

Validation does not silently replace a Result. Automatic correction is allowed only where it is explicitly part of an approved Calculation Method.

## 60. Validation Result Structure

Logical structure:

```text
ValidationResult
├── RuleID
├── Severity
├── Status
├── Message
├── DatasetIndex
├── ResultName
├── Expected
├── Actual
└── Source
```

## 61. Rule IDs

Validation Rules use unique identifiers:

```text
VAL-001
VAL-002
...
```

## 62. Validation Report

The validation layer must be able to expose:

```text
Rule
Severity
Status
Result
Index
Message
```

## 63. Validation Summary

Example:

```text
Critical = 0
Error    = 0
Warning  = 2
Info     = 4
```

with:

```text
TestQualityStatus = PASS_WITH_WARNING
```

## 64. Dependency Validation

TB-023 also validates the dependency relationships established by TB-022:

```text
Result
   ↓
Declared Dependencies
```

must match the calculation dependency graph.

## 65. Snapshot Validation

Before committing a calculation snapshot, verify:

```text
All Required Results Valid?
All Critical Rules Passed?
Dependency Versions Match?
```

## 66. Snapshot Commit Rule

If final Validation fails:

```text
Current Snapshot = FAILED
```

The previous Valid Snapshot remains preserved for audit.

## 67. Report Gate

The Report layer must evaluate `TestQualityStatus` and the required-result policy before presenting a final accepted result.

## 68. Report with Warning

`PASS_WITH_WARNING` may generate a Report, provided the warning remains traceable.

## 69. Report with FAIL

Invalid Results must not be presented as Valid Results in a failed Test Package.

## 70. Report with INCOMPLETE

Missing mandatory Results must be represented as `N/A`, `Not Available` or `Incomplete` according to the Report template, never as zero.

## 71. Audit Chain

```text
Raw TXT
 ↓
Dataset
 ↓
Calculation
 ↓
Event
 ↓
Result
 ↓
Validation Rule
 ↓
Quality Status
 ↓
Report
```

## 72. Core Principle

```text
Calculated ≠ Valid
```

The final validity concept is:

```text
Valid Result
=
Calculated
+
Consistent
+
Traceable
+
Method-Compliant
```

## 73. Freeze Decisions

| ID | Decision |
|---|---|
| D-453 | Validation is an independent Layer after Calculation. |
| D-454 | Validation does not replace the Calculation Engine. |
| D-455 | Raw Dataset is never modified by Validation. |
| D-456 | Missing Data is distinct from zero. |
| D-457 | A Result without a valid required dependency is NOT_AVAILABLE. |
| D-458 | An Invalid dependency cannot produce a VALID dependent Result. |
| D-459 | Event ordering is validated. |
| D-460 | Extensometer Release and Fracture are independent Events. |
| D-461 | Rm and Fracture are independent Events. |
| D-462 | FractureIndex is not necessarily LastDatasetIndex. |
| D-463 | RmIndex must precede FractureIndex when both are required by the Method. |
| D-464 | Rm is validated against Maximum Valid Engineering Stress according to Method. |
| D-465 | Rp0.2 without a valid intersection is NOT_AVAILABLE. |
| D-466 | Young's Modulus requires a valid Elastic Region. |
| D-467 | Stress without valid Area is INVALID. |
| D-468 | Stress is not required to be monotonic. |
| D-469 | Strain Source boundaries are validated. |
| D-470 | A Source Switch discontinuity is not automatically an Error. |
| D-471 | A% uses physical L0 and L_after rather than the last curve strain. |
| D-472 | Invalid L_after makes A% INVALID. |
| D-473 | A% without required Fracture Finalization is an inconsistent state. |
| D-474 | Graph Correction is independent and auditable. |
| D-475 | Missing optional Material Library data does not invalidate independent Results. |
| D-476 | Operator Override preserves the Original Value. |
| D-477 | Silent Correction is prohibited. |
| D-478 | Validation Rules have unique RuleIDs. |
| D-479 | Validation Severity uses INFO/WARNING/ERROR/CRITICAL. |
| D-480 | Result Status uses VALID/VALID_WITH_WARNING/INVALID/NOT_AVAILABLE/OVERRIDDEN. |
| D-481 | Test Quality Status uses PASS/PASS_WITH_WARNING/FAIL/INCOMPLETE. |
| D-482 | An invalid snapshot cannot overwrite a previous Valid Snapshot. |
| D-483 | Reporting must respect Test Quality Status. |
| D-484 | Calculated does not mean Valid. |
| D-485 | A Valid Result must be Calculated, Consistent, Traceable and Method-Compliant. |

## 74. Status

**Approved / Frozen — TB-023.**
