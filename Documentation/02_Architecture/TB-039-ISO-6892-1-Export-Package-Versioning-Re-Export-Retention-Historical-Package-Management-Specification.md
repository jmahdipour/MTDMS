# TB-039 — ISO 6892-1 Export Package Versioning, Re-Export, Retention & Historical Package Management Specification

**Status:** Approved / Frozen  
**Parent:** TB-038 / TB-037 / TB-036 / TB-035 / TB-034  
**Scope:** Excel 2019 VBA Add-in — exported TXT-file tensile-test analysis only  
**UI:** Excel Ribbon / English / LTR

## 1. Purpose

Defines versioning, re-export, retention and historical management rules for ISO 6892-1 Export Bundles. Historical Bundles are retained and are never silently overwritten or deleted as part of normal re-export.

## 2. Core Principles

- `PackageID` identifies the analytical Result Package.
- `BundleID` identifies one concrete Export Bundle.
- Re-export creates a new BundleID.
- Existing committed Bundles remain immutable.
- Exporting again does not modify the underlying analytical Result Package.
- Historical Bundles remain traceable to their PackageVersion, Export Profiles and Verification records.

## 3. Package vs Bundle Version

`PackageVersion` identifies the version of the persisted Result Package.

`BundleID` identifies a concrete export instance.

They are intentionally different:

```text
PackageID = MTDMS-2026-000184
PackageVersion = 3
BundleID = EXP-BND-2026-000184-004
```

A new export of the same PackageVersion does not require a new analytical PackageVersion; it requires a new BundleID.

## 4. Bundle Identity

Every committed Bundle has a unique:

```text
BundleID
```

Example:

```text
EXP-BND-2026-000184-001
EXP-BND-2026-000184-002
EXP-BND-2026-000184-003
```

BundleID is never reused.

## 5. Re-Export

A Re-Export is a new Export operation against an existing eligible Package.

```text
Existing Package
      ↓
New Export Operation
      ↓
New BundleID
```

The previous Bundle remains available.

## 6. Re-Export Does Not Mean Reanalysis

A failed file export or a request to create another identical export must not trigger analytical recalculation by default.

```text
Export Failure
    ↓
Retry Export
```

not:

```text
Export Failure
    ↓
Reanalysis
```

Reanalysis is governed by TB-028 through TB-031 and occurs only when the underlying analytical Package is intentionally changed or invalidated.

## 7. Package Version Change

A new `PackageVersion` is required when the persisted analytical content or controlled Package metadata changes in a manner defined by the Package lifecycle contract.

A new export file alone does not create a new PackageVersion.

## 8. Export Profile Version Change

Changing an Export Profile or its serialization contract creates a new `ProfileVersion` but does not automatically modify the PackageVersion.

Example:

```text
PackageVersion = 3
ResultProfileVersion = 1.0
```

can later become:

```text
PackageVersion = 3
ResultProfileVersion = 1.1
```

with a new BundleID.

## 9. Schema Version Change

Schema changes are recorded independently from PackageVersion.

Every Bundle must retain the exact SchemaVersion used to generate each file.

## 10. Historical Bundle Immutability

After `COMMITTED`, a Bundle is immutable.

The following operations are prohibited on a committed Bundle:

```text
UPDATE
OVERWRITE
RENAME-IN-PLACE
DELETE-BY-REEXPORT
```

Any corrected or regenerated output creates a new Bundle.

## 11. Bundle States

```text
CREATING
GENERATING
VALIDATING
VALID
COMMITTED
FAILED
INVALID
MODIFIED
SUPERSEDED
```

`SUPERSEDED` is informational and does not mean the historical Bundle is deleted or invalidated.

## 12. Superseded Bundle

A Bundle may be marked `SUPERSEDED` when a newer Bundle is designated as the preferred/current export for the same Package.

The old Bundle remains readable and auditable.

## 13. Invalid Bundle

A Bundle that fails verification is not a valid Final Export.

Its metadata may be retained for audit purposes, but it must not be represented as the current valid Bundle.

## 14. Modified Bundle

If a committed file is externally modified and its integrity verification fails, the Bundle is marked:

```text
MODIFIED
```

The original Manifest and Audit History are retained.

## 15. No Silent Repair

A modified historical Bundle must not be repaired in place.

Corrective action is:

```text
Detect
 ↓
Record
 ↓
Mark Modified
 ↓
Generate New Bundle if required
```

## 16. Current Bundle Selection

A Package may have multiple committed Bundles. The system may designate one as the current/preferred export using Bundle Registry metadata.

Selection does not delete or rewrite historical Bundles.

## 17. Bundle Registry

The internal Export Registry should retain at least:

```text
BundleID
PackageID
PackageVersion
BundleStatus
CreatedDateTime
CommittedDateTime
GeneratedBy
VerificationID
VerificationStatus
PreferredFlag
SupersedesBundleID
SupersededByBundleID
```

## 18. Bundle Relationship

Historical relationship example:

```text
Package MTDMS-2026-000184 / Version 3
       │
       ├── Bundle-001
       ├── Bundle-002
       ├── Bundle-003
       └── Bundle-004  ← Preferred
```

## 19. Supersession Chain

If a Bundle is replaced by a later export:

```text
Bundle-001
    ↓ superseded by
Bundle-002
    ↓ superseded by
Bundle-003
```

The chain must remain traceable.

## 20. Package Version History

A Package may have multiple versions:

```text
Package
 ├── Version 1
 ├── Version 2
 └── Version 3
```

Exports must explicitly identify the PackageVersion they represent.

## 21. Version Isolation

A Bundle belonging to PackageVersion 3 must never contain files generated from PackageVersion 2.

Cross-version mixing is a blocking integrity error.

## 22. Historical Export Readability

Historical committed Bundles must remain machine-readable according to the Schema/Profile version recorded in their Manifest.

The system must not silently reinterpret old files using a newer Schema.

## 23. Backward Compatibility

When a new application version opens an older Bundle:

```text
Read Original SchemaVersion
Read Original ProfileVersion
```

must occur before interpretation.

Migration, if required, must create a new representation rather than rewriting the original historical Bundle.

## 24. No Historical Overwrite

The following is prohibited:

```text
Bundle-001 committed
       ↓
Export again
       ↓
Overwrite Bundle-001
```

Correct behavior:

```text
Bundle-001 committed
       ↓
Export again
       ↓
Bundle-002 created
```

## 25. Re-Export Naming

Every Re-Export receives a unique BundleID and therefore unique file names:

```text
EXP-BND-2026-000184-004_RESULT.csv
EXP-BND-2026-000184-004_DATASET.csv
EXP-BND-2026-000184-004_AUDIT.csv
EXP-BND-2026-000184-004_MANIFEST.csv
```

## 26. Export Timestamp

Bundle creation and commit timestamps are retained separately where required:

```text
CreatedDateTime
CommittedDateTime
```

These represent export lifecycle events, not the original TestDate.

## 27. Actor Traceability

Every Export/Re-Export must identify the Actor or approved System identity that initiated the operation.

## 28. Verification Dependency

A Bundle cannot become `COMMITTED` unless the Verification status from TB-038 is successful.

```text
GENERATED
   ↓
VERIFIED
   ↓
COMMITTED
```

## 29. Re-Verification

A committed Bundle may be verified again without creating a new Bundle.

Each verification receives a new `VerificationID`; historical verification records are retained.

## 30. Retention Principle

Normal application operations must not delete historical committed Bundles.

Retention/deletion, if later required by an explicit organizational retention policy, must be handled by a separate controlled retention process and must produce an auditable event.

## 31. No Automatic Purge

MVP does not perform automatic purge based solely on:

```text
Age
Number of Bundles
Disk Space
Newer Bundle Exists
```

## 32. Controlled Retention Policy

Future retention policy may define:

```text
RetentionPeriod
RetentionClass
ArchiveLocation
LegalHold
DeletionApproval
DeletionDate
```

but these are outside the normal Re-Export operation.

## 33. Legal/Quality Hold

If a Bundle or Package is under a controlled Hold, it must not be deleted or archived in a way that breaks traceability.

MVP supports a logical:

```text
RetentionHold = TRUE/FALSE
```

field in the internal Registry.

## 34. Archive

Archiving a Bundle must preserve:

```text
BundleID
PackageID
PackageVersion
Manifest
All Export Files
Hashes
Verification History
Audit History
```

Archive is relocation/storage management, not modification of the Bundle contents.

## 35. Archive Integrity

Archived Bundles remain subject to the same SHA-256 verification rules defined by TB-038.

## 36. Restore

Restoring an archived Bundle must not change its BundleID or PackageVersion.

A restored Bundle remains the same historical Bundle.

## 37. Re-Export After Restore

A new export after restore creates a new BundleID.

The restored historical Bundle is not overwritten.

## 38. Duplicate Content

Two Bundles may contain byte-identical files. This is not an error if they have different BundleIDs and independent Export metadata.

## 39. Duplicate Hash

Identical file hashes across different Bundles are allowed when the content is genuinely identical.

Hash equality does not imply BundleID equality.

## 40. Package Change After Export

If a Package is revised through an approved Review/Override/Reanalysis workflow, a new PackageVersion is created according to the lifecycle rules.

Any subsequent export references the new PackageVersion.

## 41. Old Version Exports

Exports of previous PackageVersions remain valid historical records unless their own integrity verification fails.

Example:

```text
Package v2 → Bundle-002
Package v3 → Bundle-005
```

Both remain traceable.

## 42. Current Result Rule

The application must never infer the current Result solely from the newest file on disk.

Current/Preferred Bundle is determined by controlled Package/Export Registry metadata.

## 43. Audit Events

Minimum lifecycle events:

```text
EXPORT_BUNDLE_CREATED
EXPORT_BUNDLE_VERIFIED
EXPORT_BUNDLE_COMMITTED
EXPORT_BUNDLE_REEXPORTED
EXPORT_BUNDLE_SUPERSEDED
EXPORT_BUNDLE_MARKED_INVALID
EXPORT_BUNDLE_MARKED_MODIFIED
EXPORT_BUNDLE_ARCHIVED
EXPORT_BUNDLE_RESTORED
EXPORT_BUNDLE_RETENTION_HOLD
EXPORT_BUNDLE_RETENTION_RELEASED
```

## 44. Re-Export Audit Link

`EXPORT_BUNDLE_REEXPORTED` must reference:

```text
PreviousBundleID
NewBundleID
PackageID
PackageVersion
Actor
Timestamp
Reason
```

where applicable.

## 45. Supersession Audit Link

A supersession Event must record:

```text
SupersededBundleID
ReplacementBundleID
Actor
Timestamp
Reason
```

## 46. Retention Event

Any controlled archive/deletion operation must be auditable.

Deletion is not part of normal Export and must require an explicit retention workflow.

## 47. VBA Architecture

Recommended modules:

```text
modExportVersionController
modBundleRegistry
modBundleHistory
modBundleRetention
modBundleArchive
modBundleSupersession
modReExportController
modExportHistoryAudit
```

## 48. Public VBA Contract

```text
CreateReExport(PackageID, PackageVersion, ProfileSetID) As BundleResult
GetBundleHistory(PackageID) As BundleHistory
SetPreferredBundle(BundleID) As Boolean
MarkBundleSuperseded(BundleID, ReplacementBundleID) As Boolean
ArchiveBundle(BundleID) As ArchiveResult
RestoreBundle(BundleID) As RestoreResult
```

## 49. Re-Export Preconditions

Before Re-Export:

```text
Package Exists
PackageVersion Exists
Package Eligible For Export
Release Gate Passed
Required Export Profiles Available
```

must be true.

## 50. Re-Export Failure

If Re-Export fails:

- Existing committed Bundles remain untouched.
- Failed temporary output is not registered as Final.
- Failure is recorded in Audit History.
- Retry creates a new Export operation.

## 51. Error Codes

```text
EXP-VER-001 PACKAGE_VERSION_NOT_FOUND
EXP-VER-002 BUNDLE_ID_DUPLICATE
EXP-VER-003 HISTORICAL_BUNDLE_MODIFICATION
EXP-VER-004 VERSION_MISMATCH
EXP-VER-005 PROFILE_VERSION_INVALID
EXP-VER-006 REEXPORT_NOT_ELIGIBLE
EXP-VER-007 PREVIOUS_BUNDLE_NOT_FOUND
EXP-VER-008 SUPERSESSION_INVALID
EXP-VER-009 RETENTION_HOLD_ACTIVE
EXP-VER-010 ARCHIVE_ERROR
EXP-VER-011 RESTORE_ERROR
EXP-VER-012 HISTORY_CHAIN_ERROR
EXP-VER-013 EXPORT_REGISTRY_ERROR
```

## 52. Acceptance Criteria

TB-039 is accepted when:

```text
✓ PackageVersion and BundleID are independent
✓ Every Re-Export creates a new BundleID
✓ Existing Bundles are never silently overwritten
✓ Historical Bundles remain traceable
✓ PackageVersion is recorded in every Bundle
✓ ProfileVersion is recorded in every Bundle
✓ SchemaVersion is recorded in every Bundle
✓ Supersession chain is traceable
✓ Verification history is retained
✓ Retention does not run automatically in MVP
✓ Archive/Restore preserves Bundle identity
✓ External modification remains detectable
✓ Re-Export does not force reanalysis
✓ Failed Re-Export does not affect previous Bundles
✓ Current Bundle is selected by Registry metadata
✓ All lifecycle events are auditable
```

## 53. Freeze Decisions

| ID | Decision |
|---|---|
| D-825 | PackageVersion and BundleID are independent identifiers. |
| D-826 | Every Re-Export creates a new BundleID. |
| D-827 | Committed Bundles are immutable. |
| D-828 | Re-Export never silently overwrites a historical Bundle. |
| D-829 | Re-Export does not trigger analytical recalculation by default. |
| D-830 | Package changes follow the controlled PackageVersion lifecycle. |
| D-831 | Export Profile and Schema versions are recorded independently. |
| D-832 | Historical Bundles remain traceable to their PackageVersion. |
| D-833 | Superseded Bundles are retained. |
| D-834 | Invalid/Modified Bundles are retained as historical evidence but are not treated as valid current exports. |
| D-835 | Current/Preferred Bundle is determined by controlled Registry metadata, not file modification time. |
| D-836 | MVP has no automatic purge. |
| D-837 | Retention/deletion requires a separate controlled and auditable workflow. |
| D-838 | Archive and Restore preserve BundleID and PackageVersion. |
| D-839 | Re-Export after Restore creates a new BundleID. |
| D-840 | Duplicate content across Bundles is permitted. |
| D-841 | Duplicate file hashes across different Bundles are permitted. |
| D-842 | Re-Export and Supersession relationships are recorded in Audit History. |
| D-843 | Verification history is retained for each Bundle. |
| D-844 | All rules apply only to exported TXT-file tensile-test analysis. |

**Status: Approved / Frozen — TB-039.**
