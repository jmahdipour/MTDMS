# TB-029 — ISO 6892-1 Review Session Data Model, Override Schema & Audit Persistence Specification

**Status:** Approved / Frozen  
**Parent:** TB-028  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in

## 1. Purpose

Defines the persisted data model for Review Sessions, Manual Overrides, Audit Trail, recalculation, validation and Review Snapshots.

**Core rule:** Raw Dataset is immutable. Review is a persisted analytical layer over the Dataset.

## 2. Persistence Architecture

```text
TXT Source
   ↓
Raw Dataset
   ↓
Normalized Dataset
   ↓
Analysis Package
   ├── Review Session
   │    ├── Override
   │    ├── Audit
   │    └── Validation
   ↓
Final Result Version
```

## 3. Package Identity

```text
PackageID
PackageVersion
TestID
SourceFileID
```

## 4. ReviewSession

```text
ReviewSessionID
PackageID
PackageVersion
SessionVersion
OperatorID
StartTimestamp
EndTimestamp
Status
ReviewReason
ParentSessionID
```

Status:

```text
OPEN
COMPLETED
CANCELLED
SUPERSEDED
```

## 5. Override

```text
OverrideID
ReviewSessionID
PackageID
PackageVersion
OverrideType
ObjectType
ObjectID
AutomaticValue
OperatorValue
FinalValue
Unit
ReasonCode
ReasonText
Status
CreatedBy
CreatedAt
ValidatedAt
```

Override types:

```text
EVENT_OVERRIDE
BOUNDARY_OVERRIDE
PARAMETER_OVERRIDE
GRAPH_CORRECTION
MEASUREMENT_OVERRIDE
```

## 6. Object Types

```text
TEST_START
EXTENSOMETER_RELEASE
YIELD
RP02
ELASTIC_REGION
RM
FRACTURE
SECONDARY_GAUGE_LENGTH
HORIZONTAL_AXIS_CORRECTION
```

## 7. Value Retention

Automatic, Operator and Final values are all retained.

Example:

```text
Automatic = 1532
Operator  = 1541
Final     = 1541
```

Numeric Overrides must include their Unit. Dataset indexes use `INDEX`.

## 8. Reason Codes

Controlled vocabulary includes:

```text
EVENT_CORRECTION
FRACTURE_CORRECTION
EXTENSOMETER_BOUNDARY_CORRECTION
YIELD_CORRECTION
RM_CORRECTION
GAUGE_LENGTH_CORRECTION
GRAPH_CORRECTION
OPERATOR_REVIEW
AUTOMATIC_DETECTION_AMBIGUOUS
```

`ReasonText` stores the Operator explanation.

## 9. Override Status

```text
PROPOSED
VALIDATING
VALID
INVALID
ACCEPTED
REJECTED
CANCELLED
SUPERSEDED
```

## 10. Override Lifecycle

```text
PROPOSED → VALIDATING → VALID → ACCEPTED
```

Invalid path:

```text
PROPOSED → VALIDATING → INVALID → REJECTED
```

## 11. AuditRecord

Audit is independent of Override.

```text
AuditID
PackageID
PackageVersion
ReviewSessionID
OverrideID
OperatorID
Timestamp
Action
ObjectType
ObjectID
OldValue
NewValue
ReasonCode
ReasonText
```

## 12. Audit Actions

```text
REVIEW_OPENED
VALUE_ACCEPTED
OVERRIDE_CREATED
OVERRIDE_MODIFIED
OVERRIDE_REJECTED
OVERRIDE_ACCEPTED
RECALCULATION_STARTED
RECALCULATION_COMPLETED
VALIDATION_STARTED
VALIDATION_COMPLETED
REVIEW_COMPLETED
REVIEW_CANCELLED
PACKAGE_FINALIZED
PACKAGE_RELEASED
```

## 13. Audit Immutability

Audit records are Append-Only. Existing Audit records are never updated or deleted. A new event creates a new Audit record.

## 14. OverrideDependency

```text
OverrideID
AffectedObjectType
AffectedObjectID
DependencyLevel
RecalculationRequired
```

Dependency levels:

```text
DIRECT
INDIRECT
SECONDARY
```

Example:

```text
ExtensometerRelease
 ↓ DIRECT
Strain
 ↓ INDIRECT
YoungModulus
 ↓ SECONDARY
HorizontalAxisCorrection
```

## 15. CalculationRun

```text
CalculationRunID
PackageID
PackageVersion
ReviewSessionID
TriggeredBy
StartTimestamp
EndTimestamp
Status
CalculationVersion
```

Trigger examples:

```text
NEW_IMPORT
EVENT_OVERRIDE
BOUNDARY_OVERRIDE
PARAMETER_OVERRIDE
MEASUREMENT_OVERRIDE
GRAPH_CORRECTION
REANALYSIS
```

Status:

```text
STARTED
COMPLETED
FAILED
CANCELLED
```

## 16. ValidationRun

```text
ValidationRunID
PackageID
PackageVersion
ReviewSessionID
CalculationRunID
StartTimestamp
EndTimestamp
Status
ValidationVersion
```

Status:

```text
PASS
PASS_WITH_WARNING
FAIL
```

## 17. ValidationIssue

```text
ValidationIssueID
ValidationRunID
Severity
RuleID
ObjectType
ObjectID
Message
Status
```

Severity:

```text
INFO
WARNING
CRITICAL
```

## 18. ReviewSnapshot

At Review completion, the accepted analytical state is snapshotted:

```text
ReviewSnapshotID
ReviewSessionID
PackageID
PackageVersion
CreatedAt
```

Snapshot includes:

```text
Final Events
Final Parameters
Final Measurements
Final Results
Validation Status
```

The snapshot references RawDataset rather than creating an editable RawDataset copy.

## 19. Result Provenance

Every Final Result must trace through its CalculationRun and, where applicable, Override:

```text
A%
 ↓
CalculationRunID
 ↓
OverrideID
 ↓
L_after
 ↓
ReviewSessionID
```

## 20. Package Versioning

Versions are immutable historical records:

```text
Package V1
Package V2
Package V3
```

Each version records:

```text
ParentVersion
CreatedAt
CreatedBy
ChangeReason
AnalysisVersion
```

Previous versions are retained and may become `SUPERSEDED`.

## 21. Current Version

A Package has exactly one Current Version, while all historical versions remain persisted.

## 22. Cancelled / Superseded Overrides

Cancelled and Superseded Overrides are retained for auditability and are not physically deleted.

## 23. Transactional Persistence

Creating an Override is atomic:

```text
BEGIN
 ↓
Create Override
 ↓
Create Audit
 ↓
Create Dependency
 ↓
COMMIT
```

Failure causes Rollback.

## 24. Recalculation Transaction

```text
BEGIN
 ↓
Load Accepted Overrides
 ↓
Calculate
 ↓
Validate
 ↓
Persist Results
 ↓
Persist CalculationRun
 ↓
COMMIT
```

Failure causes Rollback.

## 25. Review Completion Transaction

```text
All Overrides Valid
 ↓
Recalculation Complete
 ↓
Validation Complete
 ↓
No Blocking Issue
 ↓
Create Snapshot
 ↓
COMMIT
```

## 26. Excel 2019 Architecture

Logical service chain:

```text
Ribbon
 ↓
Review Controller
 ↓
Review Session Service
 ↓
Override Service
 ↓
Calculation Engine
 ↓
Validation Engine
 ↓
Persistence Layer
```

## 27. SQLite Storage

If SQLite is used, the following logical tables are required:

```text
ReviewSessions
Overrides
AuditRecords
OverrideDependencies
CalculationRuns
ValidationRuns
ValidationIssues
ReviewSnapshots
```

Existing Package/Version structures from TB-025 remain the parent persistence layer.

## 28. Key and Relationship Rules

Each persisted entity has an independent primary key:

```text
ReviewSessionID
OverrideID
AuditID
CalculationRunID
ValidationRunID
ValidationIssueID
ReviewSnapshotID
```

Core relation:

```text
Package
 ↓
ReviewSession
 ↓
Override
 ↓
Audit
```

## 29. No Physical Deletion

Review, Override and Audit history must not be removed by ordinary Delete operations. Status transitions such as `CANCELLED` and `SUPERSEDED` are used instead.

## 30. Review Query Requirement

The system must be able to answer for any Package:

```text
Who reviewed it?
When?
What was automatic?
What changed?
Why?
Which Results changed?
Which calculations ran?
Which validations ran?
What is the current version?
```

## 31. MVP Tables

| Table | Purpose |
|---|---|
| `ReviewSessions` | Review lifecycle |
| `Overrides` | Operator changes |
| `AuditRecords` | Immutable audit |
| `OverrideDependencies` | Affected Results |
| `CalculationRuns` | Recalculation trace |
| `ValidationRuns` | Validation execution |
| `ValidationIssues` | Errors / Warnings |
| `ReviewSnapshots` | Accepted Review state |

## 32. Minimum Override Schema

```text
OverrideID
ReviewSessionID
OverrideType
ObjectType
ObjectID
AutomaticValue
OperatorValue
FinalValue
Unit
ReasonCode
ReasonText
Status
CreatedBy
CreatedAt
```

## 33. Minimum Audit Schema

```text
AuditID
ReviewSessionID
OverrideID
OperatorID
Timestamp
Action
ObjectType
ObjectID
OldValue
NewValue
ReasonCode
ReasonText
```

## 34. Integrity Rules

The system rejects invalid persistence relationships such as:

```text
Override without ReviewSession
Audit without Override/Session
Dependency without Override
CalculationRun without PackageVersion
ValidationRun without required CalculationRun
Snapshot without Completed Review
```

## 35. Complete Example

```text
Package V1
   ↓
ReviewSession RS-001
   ↓
Override OVR-001
   ├── ExtensometerRelease 840 → 862
   └── Audit AUD-001
   ↓
OverrideDependency
   ├── Strain
   ├── YoungModulus
   ├── Rp0.2
   └── A%
   ↓
CalculationRun CR-001
   ↓
ValidationRun VR-001
   ↓
ReviewSnapshot SNAP-001
   ↓
Package V2
```

## 36. Scope Exclusions

TB-029 does not define:

- PLC
- Machine Control
- Real-Time Acquisition
- TXT modification
- LIMS
- Cloud services
- Electronic Signature
- Detailed UI design
- Detailed SQL implementation

This document defines the Data Model and Persistence Contract, not final application code.

## 37. Freeze Decisions

| ID | Decision |
|---|---|
| D-605 | ReviewSession is an independent persisted entity. |
| D-606 | Every Override has an independent identifier. |
| D-607 | AutomaticValue, OperatorValue and FinalValue are all retained. |
| D-608 | Audit is persisted independently from Override. |
| D-609 | Audit is Append-Only. |
| D-610 | RawDataset is never modified by Review. |
| D-611 | OverrideDependency records affected Results. |
| D-612 | Recalculation has an independent CalculationRun. |
| D-613 | Validation has an independent ValidationRun. |
| D-614 | ValidationIssue is persisted independently for each warning/error. |
| D-615 | ReviewSnapshot records the accepted Review state. |
| D-616 | ReviewSnapshot does not create an editable RawDataset copy. |
| D-617 | Historical Package Versions are retained and may become Superseded. |
| D-618 | Cancelled Overrides are retained. |
| D-619 | Superseded Overrides are retained. |
| D-620 | Override persistence is transactional. |
| D-621 | Recalculation persistence is atomic. |
| D-622 | Review completion requires successful Recalculation and Validation. |
| D-623 | A Package has exactly one Current Version. |
| D-624 | Review, Override and Audit data must remain recoverable and traceable. |
| D-625 | Persistence is designed for Excel 2019 VBA Add-in architecture. |
| D-626 | SQLite, if used, is a Storage Layer and not the Analysis Model. |
| D-627 | All persistence defined here applies only to exported TXT-file analysis. |

**Status: Approved / Frozen — TB-029.**
