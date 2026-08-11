# TB-036 — ISO 6892-1 Audit Export & Review/Override History CSV Specification

**Status:** Approved / Frozen  
**Parent:** TB-035 / TB-029 / TB-030 / TB-031 / TB-034  
**Scope:** Excel 2019 VBA Add-in — exported TXT-file tensile-test analysis only  
**UI:** Excel Ribbon / English / LTR

## 1. Purpose

Defines the contractual CSV format and traceability rules for Audit Trail and Review/Override History. Audit Export is distinct from RESULT.csv and DATASET.csv and records what happened, who performed it, when it occurred, and what changed.

## 2. Audit Immutability

Audit Records are append-only. Existing Events are never updated, deleted, renumbered or overwritten. Corrections are represented by new Events.

## 3. Source of Truth

Audit Export reads only from persisted Audit History associated with the Result Package. Worksheet cells, Reports and transient UI state are not authoritative Audit sources.

## 4. Audit CSV Profile

```text
ProfileID = ISO6892_AUDIT_CSV
ProfileVersion = 1.0
Format = CSV
Encoding = UTF-8
Delimiter = ,
DecimalSeparator = .
UTF-8 BOM = enabled
```

## 5. MVP Header

```text
AuditID,PackageID,PackageVersion,TestID,ReviewSessionID,Timestamp,Actor,EventType,FieldID,OldValue,NewValue,Reason,Source,Severity,ValidationStatus,ReleaseImpact
```

The MVP profile contains exactly 16 columns.

## 6. Field Contract

| Field | Purpose |
|---|---|
| AuditID | Unique Event identifier |
| PackageID | Result Package identifier |
| PackageVersion | Package version |
| TestID | Test identifier |
| ReviewSessionID | Review/Override session identifier |
| Timestamp | Event timestamp |
| Actor | Internal actor/operator identifier |
| EventType | Event classification |
| FieldID | Affected field, where applicable |
| OldValue | Value before change |
| NewValue | Value after change |
| Reason | Mandatory reason for manual Override |
| Source | Event origin |
| Severity | INFO/WARNING/ERROR/CRITICAL |
| ValidationStatus | Validation state associated with Event |
| ReleaseImpact | Effect on Release |

## 7. AuditID

Every Event has a unique AuditID. AuditIDs are never reused.

## 8. Event Ordering

Export order is deterministic:

```text
Timestamp ASC
AuditID ASC
```

EventType, Actor or FieldID must not determine authoritative ordering.

## 9. Timestamp

Use locale-independent format:

```text
YYYY-MM-DDTHH:MM:SS
```

This represents Event time, not TestDate.

## 10. Actor

Actor identifies the internal operator/reviewer/system responsible for the Event. System-generated Events use `System` or the approved system Actor identifier.

## 11. EventType

MVP EventTypes:

```text
PACKAGE_CREATED
PACKAGE_OPENED
REVIEW_STARTED
REVIEW_COMPLETED
REVIEW_CANCELLED
OVERRIDE_CREATED
OVERRIDE_VALIDATED
OVERRIDE_REJECTED
OVERRIDE_APPLIED
OVERRIDE_REVERSED
REANALYSIS_STARTED
REANALYSIS_COMPLETED
VALIDATION_STARTED
VALIDATION_FAILED
VALIDATION_PASSED
RELEASE_BLOCKED
RELEASE_APPROVED
RELEASE_REJECTED
EXPORT_STARTED
EXPORT_COMPLETED
EXPORT_FAILED
```

## 12. Manual Override

Every manual Override must record:

```text
FieldID
OldValue
NewValue
Reason
Actor
Timestamp
ReviewSessionID
```

An Override without a valid Reason is rejected and cannot contribute to Release.

## 13. OldValue

OldValue is the authoritative value immediately before the Override. Report-display rounding must not replace analytical precision.

## 14. NewValue

NewValue is the explicitly entered or selected value proposed by the Operator/Reviewer and must pass applicable validation before Release.

## 15. FieldID

FieldID must reference the established data contract. Examples include Result fields such as `Rp0.2`, `Rm`, `YieldStrength`, `YoungModulus` and `ElongationAfterFracture`.

## 16. Graph Override Fields

Graph-related Overrides must remain distinguishable from Result Overrides. Examples:

```text
GRAPH-YIELD-MARKER
GRAPH-ELASTIC-BOUNDARY
GRAPH-FRACTURE-BOUNDARY
GRAPH-STRAIN-CORRECTION
```

## 17. Reanalysis Trace

An Override requiring reanalysis must be followed by traceable Events such as:

```text
OVERRIDE_APPLIED
REANALYSIS_STARTED
REANALYSIS_COMPLETED
VALIDATION_STARTED
VALIDATION_PASSED
```

These Events must not be collapsed into one final record.

## 18. ReviewSessionID

Every Review Session has a unique identifier, for example:

```text
REV-2026-000184-001
```

A Package may contain multiple Review Sessions. Historical Sessions are retained.

## 19. Review Session Lifecycle

```text
NOT_STARTED
    ↓
OPEN
    ↓
IN_REVIEW
    ↓
REANALYSIS
    ↓
VALIDATION
    ↓
COMPLETED
```

Alternative terminal state:

```text
CANCELLED
```

## 20. Override Reversal

An incorrect Override is reversed by a new `OVERRIDE_REVERSED` Event. The original Event remains unchanged.

## 21. Release Impact

Permitted MVP values:

```text
NONE
WARNING
BLOCKING
REQUIRES_REANALYSIS
REQUIRES_REVALIDATION
```

## 22. Severity

Permitted values:

```text
INFO
WARNING
ERROR
CRITICAL
```

## 23. Event Validation

Every Audit Event requires at minimum:

```text
AuditID
PackageID
Timestamp
Actor
EventType
Severity
```

Override Events additionally require FieldID, OldValue/NewValue where applicable, Reason and ReviewSessionID.

## 24. Audit Chain

The internal Audit model must preserve linkage to the preceding Event using `PreviousAuditID`. Future schema versions may additionally expose `PreviousAuditHash` and `CurrentAuditHash`.

## 25. Audit Eligibility

Audit Export is permitted for Draft, Review and Released Packages because Audit History is itself traceability evidence.

Final Result Export remains governed by the Release Gate defined by previous TBs.

## 26. Failed Operations

Failed operations are retained and exported, including:

```text
VALIDATION_FAILED
OVERRIDE_REJECTED
REANALYSIS_FAILED
EXPORT_FAILED
```

## 27. Audit Export Event

Audit Export itself must not mutate the Audit History. If the profile explicitly enables export-event logging, a separate `AUDIT_EXPORT_COMPLETED` Event may be appended.

## 28. Audit Manifest

Minimum Audit Export Manifest fields:

```text
ExportID
PackageID
AuditRecordCount
FileSize
ExportHash
GeneratedDateTime
GeneratedBy
```

## 29. Record Count Verification

After writing:

```text
ExpectedAuditRecords = ActualAuditRecords
```

Any mismatch blocks finalization of the Audit Export.

## 30. CSV Escaping

CSV escaping follows TB-034:

- Fields containing comma, quote, CR or LF are quoted.
- Embedded quotes are doubled.
- Decimal separator is always `.`.

## 31. Temporary File Transaction

```text
BEGIN
Validate Audit
Serialize
Write Temporary CSV
Verify
Hash
Commit Manifest
Rename Final
END
```

Partial temporary output must never be registered as a Final Audit Export.

## 32. Deterministic Export

The same Audit Records, Schema Version and Export Profile must produce the same Event ordering and field serialization, apart from explicitly time-dependent export metadata.

## 33. VBA Module Architecture

Recommended modules:

```text
modAuditController
modAuditRepository
modAuditSerializer
modAuditCsvWriter
modReviewSession
modOverrideManager
modAuditValidator
modAuditManifest
modAuditHash
```

## 34. VBA Public Contract

```text
ExportAudit(PackageID, ProfileID) As ExportResult
ExportReviewHistory(PackageID, ReviewSessionID, ProfileID) As ExportResult
```

The Review History export may use the same physical Audit CSV profile; EventType and ReviewSessionID distinguish Review history from other Audit Events.

## 35. ExportResult

Minimum fields:

```text
Success
ExportID
FilePath
FileName
FileSize
ExportHash
ErrorCode
ErrorMessage
```

## 36. Consistency Rules

For every `OVERRIDE_CREATED` Event:

```text
ReviewSessionID must exist
FieldID must be valid
Reason must exist
```

If ReleaseImpact requires reanalysis, corresponding Reanalysis Events must exist before Release can pass.

If ReleaseImpact requires revalidation, corresponding Validation Events must exist before Release can pass.

## 37. No Loss of History

Multiple changes to the same Result must remain separately traceable. Example:

```text
200 → 201
201 → 199
199 → 200
```

All three Events remain in Audit History.

## 38. Error Codes

```text
EXP-AUDIT-001 AUDIT_ID_DUPLICATE
EXP-AUDIT-002 AUDIT_RECORD_INVALID
EXP-AUDIT-003 AUDIT_TIMESTAMP_ERROR
EXP-AUDIT-004 AUDIT_EVENT_TYPE_ERROR
EXP-AUDIT-005 REVIEW_SESSION_INVALID
EXP-AUDIT-006 OVERRIDE_REASON_MISSING
EXP-AUDIT-007 OVERRIDE_FIELD_INVALID
EXP-AUDIT-008 REANALYSIS_TRACE_MISSING
EXP-AUDIT-009 VALIDATION_TRACE_MISSING
EXP-AUDIT-010 AUDIT_ROW_COUNT_ERROR
EXP-AUDIT-011 AUDIT_WRITE_ERROR
EXP-AUDIT-012 AUDIT_HASH_ERROR
EXP-AUDIT-013 AUDIT_VERIFICATION_ERROR
```

## 39. Freeze Decisions

| ID | Decision |
|---|---|
| D-763 | Audit Records are immutable. |
| D-764 | Audit corrections create new Events; old Events are never modified. |
| D-765 | Every Audit Event has a unique AuditID. |
| D-766 | ReviewSessionID links Review and Override Events. |
| D-767 | Manual Override requires a Reason. |
| D-768 | OldValue and NewValue must be traceable. |
| D-769 | Override Events must identify FieldID. |
| D-770 | Reanalysis Events remain separate from Override Events. |
| D-771 | Validation Events remain separate from Reanalysis Events. |
| D-772 | Release Events remain separate from Validation Events. |
| D-773 | Failed operations are retained in Audit History. |
| D-774 | Audit Export does not require Package Release. |
| D-775 | Audit Export uses UTF-8 CSV. |
| D-776 | Audit Export uses deterministic Event ordering. |
| D-777 | Audit Export uses temporary-file transaction semantics. |
| D-778 | Audit Export is hashable and auditable. |
| D-779 | Audit History cannot be reconstructed solely from the final Result. |
| D-780 | All rules apply only to exported TXT-file tensile-test analysis. |

**Status: Approved / Frozen — TB-036.**
