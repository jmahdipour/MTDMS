# TB-041 — ISO 6892-1 Export Package Backup, Disaster Recovery & Restore Integrity Specification

**Status:** Approved / Frozen  
**Parent:** TB-040 / TB-039 / TB-038 / TB-037  
**Scope:** Excel 2019 VBA Add-in — exported TXT-file tensile-test analysis only  
**UI:** Excel Ribbon / English / LTR

## 1. Purpose

Defines Backup and Disaster Recovery rules for committed Export Bundles while preserving PackageID, PackageVersion, BundleID, hashes, verification history and audit traceability.

## 2. Core Principles

- Backup and Archive are separate controls.
- A Backup has its own BackupID but preserves the original BundleID.
- Only successfully verified committed Bundles are eligible for valid Final Backup.
- Restore does not recalculate analytical results.
- Exact Restore preserves BundleID, PackageID and PackageVersion.
- Restore conflicts and hash mismatches are blocking conditions.
- Backup and Restore operations are auditable.

## 3. Backup Unit

The Backup Unit is the complete Export Bundle plus required metadata:

```text
RESULT.csv
DATASET.csv
AUDIT.csv
MANIFEST.csv
PackageID
PackageVersion
BundleID
SchemaVersion
ProfileVersion
VerificationID
VerificationStatus
Audit History
```

## 4. Backup Identity

Every Backup receives a unique `BackupID`, for example:

```text
BKP-2026-000184-001
```

`BackupID` never replaces `BundleID`.

## 5. Backup Preconditions

```text
BundleStatus = COMMITTED
AND
VerificationStatus = PASSED
```

are required for a valid Final Backup.

## 6. Backup Process

```text
Committed Bundle
↓
Pre-Backup Verification
↓
Copy
↓
Calculate Destination Hash
↓
Compare Source/Backup Hash
↓
Verify Metadata
↓
Register Backup
```

## 7. Atomic Backup

Temporary backup content must not be registered as valid. A failed/incomplete operation remains `FAILED` and is not a Restore candidate.

## 8. Backup States

```text
REQUESTED
RUNNING
VERIFYING
VALID
COMMITTED
FAILED
CORRUPTED
RESTORING
RESTORED
```

## 9. Backup Metadata

At minimum:

```text
BackupID
BundleID
PackageID
PackageVersion
BackupDateTime
BackupLocation
BackupStatus
SourceHash
BackupHash
VerificationID
CreatedBy
```

## 10. Hash Integrity

For every backed-up file:

```text
SourceHash = SHA256(SourceFile)
BackupHash = SHA256(BackupFile)
SourceHash = BackupHash
```

Hash covers the physical file bytes, including encoding, BOM, CR/LF, quoting, header and rows.

## 11. Backup Corruption

If verification fails:

```text
BackupStatus = CORRUPTED
```

The Backup must not be selected for normal Restore.

## 12. Multiple Backups

Multiple valid Backups may exist for one Bundle:

```text
Bundle-004
├── Backup-001
├── Backup-002
└── Backup-003
```

## 13. Backup Selection

Recovery selection considers:

```text
Valid
Verified
Correct PackageVersion
Correct BundleID
Newest valid Recovery Point
```

Timestamp alone is insufficient.

## 14. Disaster Recovery Triggers

Disaster Recovery may be initiated for:

```text
SOURCE_MISSING
SOURCE_CORRUPTED
STORAGE_FAILURE
ACCIDENTAL_DELETION
SYSTEM_FAILURE
OTHER
```

## 15. Restore Modes

Two modes are defined:

```text
RESTORE_EXACT
RESTORE_AS_NEW_BUNDLE
```

## 16. Exact Restore

Exact Restore is intended for Disaster Recovery and preserves:

```text
BundleID
PackageID
PackageVersion
```

## 17. Restore as New Bundle

If restored content is intentionally republished as a new Export:

```text
Backup
↓
Verify
↓
New BundleID
↓
New Export
```

This is treated as Re-Export, not historical Exact Restore.

## 18. Restore Conflict

```text
Destination Missing → Restore
Destination Same Hash → Already Restored
Destination Different Hash → BLOCK
```

The system must not silently overwrite a different existing Bundle.

## 19. Restore Verification

After Restore:

```text
File Count
File Size
SHA-256
Manifest
PackageID
BundleID
PackageVersion
SchemaVersion
ProfileVersion
```

must be verified.

## 20. Restore Commit Gate

Restore is successful only after post-restore verification passes.

## 21. Restore Audit

Every Restore records:

```text
EXPORT_BUNDLE_RESTORED
```

with:

```text
BackupID
BundleID
PackageID
PackageVersion
RestoredBy
RestoreDateTime
VerificationID
RestoreStatus
```

## 22. Disaster Recovery Audit

Minimum lifecycle events:

```text
DISASTER_RECOVERY_STARTED
DISASTER_RECOVERY_BACKUP_SELECTED
DISASTER_RECOVERY_RESTORE_STARTED
DISASTER_RECOVERY_VERIFICATION_COMPLETED
DISASTER_RECOVERY_COMPLETED
DISASTER_RECOVERY_FAILED
```

## 23. Recovery Point

Every Backup represents a Recovery Point identified by:

```text
BackupDateTime
PackageVersion
BundleID
```

## 24. Version Validation

Before Restore:

```text
Backup.PackageVersion
=
Backup.Manifest.PackageVersion
=
Expected PackageVersion
```

and:

```text
Backup.BundleID
=
Manifest.BundleID
=
ExportFiles.BundleID
```

## 25. Backup Storage

Backup Storage should be logically separate from Active Export Storage:

```text
Active Export Storage ≠ Backup Storage
```

Where organizational infrastructure permits, Backup should also be held on independently recoverable storage.

## 26. Backup Retention

Backup Retention is independent of Archive Retention.

Example:

```text
Archive Retention = 10 years
Backup Retention = 12 months
```

## 27. Backup Hold

A Backup may be protected by a controlled retention hold:

```text
BackupRetentionHold = TRUE
```

which blocks deletion.

## 28. Backup Deletion

Backup deletion follows a controlled workflow:

```text
Candidate
↓
Retention Check
↓
Hold Check
↓
Approval
↓
Delete
↓
Audit
```

## 29. Backup Tombstone

After controlled Backup deletion, Registry retains:

```text
BackupID
BundleID
DeletedDateTime
DeletedBy
DeletionReason
```

BackupID is never reused.

## 30. Periodic Backup Verification

Backups may be periodically verified independently of Restore:

```text
VerifyBackup()
↓
PASSED / CORRUPTED / MISSING
```

## 31. Backup Coverage

The Registry should expose at minimum:

```text
HasValidBackup
LastBackup
LastVerifiedBackup
BackupCount
ValidBackupCount
CorruptedBackupCount
```

## 32. Recovery Test

A controlled Recovery Test may be executed without changing the production Bundle:

```text
Backup
↓
Test Restore
↓
Verify
↓
Discard Test Restore
```

The test itself is auditable.

## 33. Recovery Test Audit

Event:

```text
DISASTER_RECOVERY_TEST
```

records:

```text
BackupID
TestDateTime
TestedBy
VerificationID
Result
```

## 34. No Silent Recovery

Restore and Disaster Recovery operations must always create Audit records.

## 35. No Silent Overwrite

A Restore may not overwrite an existing different-hash Bundle without an explicit controlled process.

## 36. VBA Modules

Recommended modules:

```text
modBackupController
modBackupRegistry
modBackupManifest
modBackupVerifier
modBackupHash
modBackupRetention
modBackupRestore
modDisasterRecovery
modRecoveryTest
modBackupAudit
```

## 37. Public VBA Contract

```text
CreateBackup(BundleID) As BackupResult
VerifyBackup(BackupID) As BackupVerificationResult
RestoreBackup(BackupID) As RestoreResult
TestRestoreBackup(BackupID) As RecoveryTestResult
SelectRecoveryBackup(PackageID, PackageVersion) As BackupSelectionResult
GetBackupHistory(BundleID) As BackupHistory
```

## 38. Acceptance Criteria

```text
✓ Backup is independent from Archive
✓ Backup has unique BackupID
✓ BundleID is preserved
✓ PackageVersion is preserved
✓ Backup is verified before registration
✓ Source and Backup SHA-256 values match
✓ Backup corruption is detectable
✓ Multiple Backups are supported
✓ Exact Restore preserves Bundle identity
✓ Restore performs integrity verification
✓ Restore conflicts are detected
✓ Silent overwrite is prohibited
✓ Disaster Recovery is audited
✓ Recovery Test is supported
✓ Backup Retention is independent
✓ Backup Hold blocks deletion
✓ Backup deletion is controlled
✓ Backup tombstones are retained
✓ Backup history remains traceable
✓ Restore never recalculates analytical Results
```

## 39. Freeze Decisions

| ID | Decision |
|---|---|
| D-864 | Backup and Archive are separate processes. |
| D-865 | Backup has an independent BackupID. |
| D-866 | Valid Final Backup requires a committed, successfully verified Bundle. |
| D-867 | Backup includes Export Files and required metadata. |
| D-868 | Source and Backup SHA-256 values must match. |
| D-869 | Multiple Backups per Bundle are allowed. |
| D-870 | Backup corruption must be detectable. |
| D-871 | Exact Restore preserves BundleID. |
| D-872 | Restore cannot silently overwrite a different-hash destination. |
| D-873 | Restore requires post-restore verification. |
| D-874 | Disaster Recovery does not recalculate Results. |
| D-875 | Disaster Recovery operations are auditable. |
| D-876 | Recovery Test is independent from the production Bundle. |
| D-877 | Backup Retention is independent of Archive Retention. |
| D-878 | Backup Hold blocks deletion. |
| D-879 | Backup deletion is controlled and auditable. |
| D-880 | BackupID is never reused. |
| D-881 | Restore conflict with a different hash is blocking. |
| D-882 | Backup Storage should be independent from Active Export Storage where possible. |
| D-883 | All rules apply only to Export Packages for TXT-file tensile-test analysis. |

**Status: Approved / Frozen — TB-041.**
