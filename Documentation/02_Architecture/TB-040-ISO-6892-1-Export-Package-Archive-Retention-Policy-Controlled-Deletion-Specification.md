# TB-040 — ISO 6892-1 Export Package Archive, Retention Policy & Controlled Deletion Specification

**Status:** Approved / Frozen  
**Parent:** TB-039 / TB-038 / TB-037  
**Scope:** Excel 2019 VBA Add-in — exported TXT-file tensile-test analysis only  
**UI:** Excel Ribbon / English / LTR

## 1. Purpose

Defines controlled rules for Archive, Retention, Restore, Retention Hold and Deletion of historical Export Bundles.

## 2. Core Principles

- Archive and Delete are separate operations.
- Archive does not change BundleID, PackageID or PackageVersion.
- Archive requires successful Bundle Verification.
- MVP has no automatic purge.
- Retention expiry makes a Bundle eligible for review, not automatically deletable.
- Controlled deletion requires approval and audit.
- Deleted Bundle identity is never reused.
- Tombstone metadata remains after deletion.

## 3. Archive

Archive is controlled relocation/storage of a committed Bundle:

```text
ACTIVE → ARCHIVED
```

The archived Bundle retains:

```text
RESULT.csv
DATASET.csv
AUDIT.csv
MANIFEST.csv
BundleID
PackageID
PackageVersion
Hashes
Verification History
Audit History
```

## 4. Archive Preconditions

Archive is permitted only when:

```text
Bundle Exists
AND Verification = PASSED
AND BundleStatus = COMMITTED
AND No Blocking Retention Condition
```

## 5. Archive Integrity

The archive operation follows:

```text
Verify Source
↓
Copy
↓
Verify Destination Size
↓
Verify Destination SHA-256
↓
Commit Archive Metadata
```

Source files are not removed before destination verification succeeds.

## 6. Archive Identity

Archive does not create a new BundleID. The original BundleID remains the permanent identity of the historical export.

## 7. Archive Location

Recommended structure:

```text
Archive\2026\MTDMS-2026-000184\EXP-BND-2026-000184-004\
    RESULT.csv
    DATASET.csv
    AUDIT.csv
    MANIFEST.csv
```

## 8. Archive Metadata

Registry stores at minimum:

```text
BundleID
PackageID
PackageVersion
ArchiveDateTime
ArchiveLocation
ArchiveStatus
ArchivedBy
VerificationID
```

## 9. Archive States

```text
NOT_ARCHIVED
ARCHIVING
ARCHIVED
ARCHIVE_VERIFICATION_FAILED
ARCHIVE_FAILED
RESTORING
RESTORED
```

## 10. Retention Classes

MVP defines:

```text
STANDARD
CONTROLLED
PERMANENT
```

## 11. Retention Metadata

```text
RetentionClass
RetentionStartDate
RetentionEndDate
RetentionHold
DeletionEligible
```

## 12. Retention Start

Default retention starts from `CommittedDateTime`, not TestDate.

## 13. Retention Eligibility

A Bundle is eligible for controlled deletion only when:

```text
RetentionPeriodExpired
AND RetentionHold = FALSE
AND NoPendingInvestigation
AND BundleNotRequired
AND DeletionApproved
```

## 14. No Automatic Purge

MVP never deletes a Bundle solely because its retention period has expired.

```text
Expired
↓
Eligible
↓
Review
↓
Approval
↓
Controlled Delete
```

## 15. Retention Hold

A Bundle can be protected by:

```text
RetentionHold = TRUE
```

Hold blocks deletion regardless of retention expiry.

## 16. Hold Reasons

```text
QUALITY_INVESTIGATION
CUSTOMER_DISPUTE
NONCONFORMANCE
AUDIT
LEGAL
MANAGEMENT
OTHER
```

## 17. Hold Identity

Each Hold has a unique `HoldID`, for example:

```text
HLD-2026-000184-001
```

## 18. Hold Lifecycle

```text
ACTIVE → RELEASED
```

After release, deletion eligibility is recalculated.

## 19. Permanent Retention

`PERMANENT` Bundles are protected from normal deletion.

## 20. Invalid / Modified Bundles

`INVALID`, `MODIFIED` and `SUPERSEDED` do not imply deletion eligibility. Historical evidence may still be required.

## 21. Restore

Restore follows:

```text
ARCHIVED
↓
RESTORE
↓
VERIFY
↓
RESTORED
```

Restore preserves:

```text
BundleID
PackageID
PackageVersion
```

## 22. Restore Verification

Restore is complete only after:

```text
File Exists
FileSize Matches
SHA-256 Matches
Manifest Valid
Package Identity Valid
```

## 23. Controlled Deletion

Deletion is an independent controlled workflow:

```text
Candidate
↓
Review
↓
Approve
↓
Delete
↓
Verify
↓
Audit
```

## 24. Separation of Duties

Controlled deletion should use:

```text
RequestedBy <> ApprovedBy
```

unless an explicitly approved organizational policy permits otherwise.

## 25. Deletion Request

Each request receives a unique `DeletionRequestID`, for example:

```text
DEL-2026-000184-001
```

States:

```text
REQUESTED
UNDER_REVIEW
APPROVED
REJECTED
EXECUTED
FAILED
CANCELLED
```

## 26. Deletion Reasons

```text
RETENTION_EXPIRED
DUPLICATE
INVALID_EXPORT
STORAGE_POLICY
OTHER
```

## 27. Deletion Verification

After deletion:

```text
FileDoesNotExist
ArchiveDirectoryDoesNotExist
RegistryStatus = DELETED
```

must be confirmed.

## 28. Tombstone

After controlled deletion, the Registry retains a minimal tombstone:

```text
BundleID
PackageID
PackageVersion
DeletedDateTime
DeletedBy
DeletionRequestID
DeletionReason
```

## 29. No Identity Reuse

Deleted BundleIDs and DeletionRequestIDs are never reused.

## 30. Audit Preservation

Deleting an Export Bundle never deletes the Audit History describing its creation, verification, archive, hold, approval or deletion.

## 31. Archive Integrity Reverification

Archived Bundles may be periodically verified:

```text
Archive Bundle
↓
SHA-256 Verification
↓
PASS / MODIFIED
```

## 32. Archive Corruption

If archived content fails verification:

```text
ArchiveStatus = ARCHIVE_CORRUPTED
```

The event is audited and recovery is evaluated from an approved source/backup.

## 33. No Silent Replacement

Corrupted archived files must not be silently replaced. Any recovery or replacement is an auditable operation.

## 34. Archive vs Backup

Archive is historical controlled storage. Backup is disaster-recovery storage. They are separate controls even if they contain identical Bundle data.

## 35. VBA Modules

Recommended modules:

```text
modRetentionController
modRetentionPolicy
modRetentionHold
modArchiveController
modArchiveVerifier
modRestoreController
modDeletionController
modDeletionApproval
modTombstoneRegistry
modRetentionAudit
```

## 36. Public VBA Contract

```text
ArchiveBundle(BundleID) As ArchiveResult
RestoreBundle(BundleID) As RestoreResult
RequestBundleDeletion(BundleID, Reason) As DeletionRequestResult
ApproveBundleDeletion(RequestID) As Boolean
ExecuteBundleDeletion(RequestID) As DeletionResult
EvaluateRetention(BundleID) As RetentionResult
SetRetentionHold(BundleID, Reason) As Boolean
ReleaseRetentionHold(HoldID) As Boolean
```

## 37. Acceptance Criteria

TB-040 is accepted when:

```text
✓ Archive preserves Bundle identity
✓ Archive is verified before source cleanup
✓ Destination hash and size are verified
✓ Restore preserves BundleID and PackageVersion
✓ Restore is integrity-verified
✓ Retention period is explicit
✓ Retention Hold blocks deletion
✓ PERMANENT packages are protected
✓ MVP has no automatic purge
✓ Deletion requires controlled approval
✓ Deletion is audited
✓ Tombstone remains after deletion
✓ Deleted IDs are never reused
✓ Invalid/Modified Bundles are not automatically deleted
✓ Superseded Bundles remain retained
✓ Archive corruption is detectable
✓ Historical traceability is preserved
✓ Archive and Backup remain logically separate
```

## 38. Freeze Decisions

| ID | Decision |
|---|---|
| D-845 | Archive and Delete are separate controlled operations. |
| D-846 | Archive does not change BundleID. |
| D-847 | Archive requires successful Bundle Verification. |
| D-848 | Destination integrity must be verified before source cleanup. |
| D-849 | Restore preserves BundleID, PackageID and PackageVersion. |
| D-850 | Restore requires post-restore Verification. |
| D-851 | MVP has no automatic deletion based only on retention expiry. |
| D-852 | Retention eligibility is distinct from deletion approval. |
| D-853 | Retention Hold blocks deletion. |
| D-854 | PERMANENT retention class is protected from normal deletion. |
| D-855 | Invalid and Modified Bundles are not automatically deleted. |
| D-856 | Superseded Bundles remain retained. |
| D-857 | Controlled deletion requires an auditable approval workflow. |
| D-858 | Tombstone metadata remains after deletion. |
| D-859 | BundleID and historical identifiers are never reused. |
| D-860 | Deletion does not erase historical Audit records. |
| D-861 | Archive integrity can be periodically re-verified. |
| D-862 | Archive and Backup are separate concepts. |
| D-863 | All rules apply only to exported TXT-file tensile-test analysis. |

**Status: Approved / Frozen — TB-040.**
