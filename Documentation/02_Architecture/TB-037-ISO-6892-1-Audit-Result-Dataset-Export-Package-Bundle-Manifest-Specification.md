# TB-037 — ISO 6892-1 Audit / Result / Dataset Export Package Bundle & Manifest Specification

**Status:** Approved / Frozen  
**Parent:** TB-036 / TB-035 / TB-034 / TB-033 / TB-032  
**Scope:** Excel 2019 VBA Add-in — exported TXT-file tensile-test analysis only  
**UI:** Excel Ribbon / English / LTR

## 1. Purpose

Defines the contractual structure for a final Export Bundle containing `RESULT.csv`, `DATASET.csv`, `AUDIT.csv` and `MANIFEST.csv`.

## 2. Core Principle

`MANIFEST.csv` is the authoritative index connecting the exported files to the Package, PackageVersion, Export Profiles, record counts, file sizes and hashes.

## 3. MVP Bundle Contents

```text
RESULT.csv
DATASET.csv
AUDIT.csv
MANIFEST.csv
```

## 4. Bundle Identity

Every bundle has a unique `BundleID`, independent of `PackageID`.

Example:

```text
EXP-BND-2026-000184-001
```

Every file also has an independent `ExportID`.

## 5. File Naming

MVP uses BundleID-prefixed names:

```text
{BundleID}_RESULT.csv
{BundleID}_DATASET.csv
{BundleID}_AUDIT.csv
{BundleID}_MANIFEST.csv
```

## 6. Manifest Header

```text
BundleID,PackageID,PackageVersion,ExportID,FileName,FileType,ProfileID,ProfileVersion,SchemaVersion,FileSize,RecordCount,ExportHash,GeneratedDateTime,GeneratedBy,ValidationStatus,ReleaseStatus
```

The MVP Manifest contains 16 columns.

## 7. Manifest File Types

```text
RESULT
DATASET
AUDIT
MANIFEST
```

## 8. Profile Mapping

```text
RESULT  → ISO6892_RESULT_CSV
DATASET → ISO6892_DATASET_CSV
AUDIT   → ISO6892_AUDIT_CSV
MANIFEST → ISO6892_MANIFEST_CSV
```

## 9. Bundle Status

MVP states:

```text
CREATING
VALIDATING
VALID
INVALID
INCOMPLETE
COMMITTED
FAILED
```

## 10. Final Bundle Eligibility

A Final Bundle requires all required files to exist and pass verification. `RESULT.csv` additionally requires the Result Release Gate to be passed.

## 11. Cross-File Identity

The following must be identical across all applicable files:

```text
PackageID
PackageVersion
TestID
```

No Bundle may mix different Package Versions.

## 12. Dataset Dependency

`DATASET.csv` must originate from the same Released Package as `RESULT.csv`.

## 13. Audit Dependency

`AUDIT.csv` must represent Audit History associated with the same PackageID and PackageVersion.

## 14. Manifest Purpose

Manifest must identify, without opening other files:

- files in the Bundle;
- FileType;
- ExportID;
- ProfileID/ProfileVersion;
- SchemaVersion;
- FileSize;
- RecordCount;
- ExportHash;
- generation metadata.

## 15. Hash Algorithm

MVP uses:

```text
SHA-256
```

Hash is calculated over the final file bytes after file verification. The hash is represented as 64 hexadecimal characters.

## 16. Manifest Self-Hash

The Manifest does not contain its own hash because that would create a circular dependency. The Manifest file hash is stored in the internal Export Registry / Bundle Commit Metadata.

## 17. Bundle Integrity

Bundle is valid only if:

```text
Manifest Exists
AND
All Required Files Exist
AND
FileSize Matches
AND
RecordCount Matches
AND
Hash Matches
AND
Cross-File Identity Matches
AND
Profile/Schema Versions Match
```

## 18. Atomic Bundle Creation

All files are created in a temporary Bundle location and committed only after complete verification.

```text
Create Temporary Bundle
    ↓
Generate RESULT
    ↓
Generate DATASET
    ↓
Generate AUDIT
    ↓
Verify Three Files
    ↓
Calculate Hashes
    ↓
Generate MANIFEST
    ↓
Verify MANIFEST
    ↓
Commit Bundle
```

## 19. No Partial Final Bundle

A Final Bundle must never expose a state such as:

```text
RESULT.csv   ✓
DATASET.csv  ✓
AUDIT.csv    ✗
MANIFEST.csv ✗
```

## 20. Record Count

Manifest stores the expected and verified record count for each export. Actual record count must equal the expected count before Commit.

## 21. File Size

FileSize is recorded in bytes after the final file is written and closed.

## 22. Hash Validation

A hash mismatch is a blocking Bundle error:

```text
BUNDLE-HASH-MISMATCH
```

The Bundle cannot be committed as Final.

## 23. Post-Commit Modification

If a committed file is externally modified, its calculated hash will no longer match the Manifest/Registry record and the Bundle must be reported as modified/invalid.

The system is not required to silently restore modified files.

## 24. Bundle Audit Events

Minimum Bundle Events:

```text
EXPORT_BUNDLE_STARTED
EXPORT_RESULT_COMPLETED
EXPORT_DATASET_COMPLETED
EXPORT_AUDIT_COMPLETED
EXPORT_MANIFEST_CREATED
EXPORT_BUNDLE_VALIDATED
EXPORT_BUNDLE_COMMITTED
EXPORT_BUNDLE_FAILED
```

## 25. Bundle Failure

Failure of any required export prevents Final Bundle Commit. The incomplete temporary Bundle is not registered as Final.

## 26. Retry

Retry uses the same Released Package and does not rerun analysis merely because file generation failed.

## 27. Re-Export

A subsequent export creates a new BundleID. Previous Bundles are retained and remain independently traceable.

## 28. Export Location

Recommended final structure:

```text
<PackageFolder>\Exports\<BundleID>\
    <BundleID>_RESULT.csv
    <BundleID>_DATASET.csv
    <BundleID>_AUDIT.csv
    <BundleID>_MANIFEST.csv
```

## 29. Bundle Builder Responsibilities

Bundle Builder may:

```text
Collect
Validate
Connect
Serialize
Hash
Verify
Commit
```

It must not calculate new analytical Results.

## 30. Worksheet Independence

Bundle generation must not use Report or Worksheet presentation cells as the authoritative source of Result/Dataset/Audit data.

## 31. Encoding

All machine-readable CSV files in the Bundle use UTF-8. UTF-8 BOM is enabled by default for Excel 2019 compatibility.

## 32. Locale Independence

Output is independent of Windows/Excel regional settings:

```text
Delimiter = ,
DecimalSeparator = .
```

## 33. Bundle Verification API

Recommended internal operations:

```text
VerifyBundleFiles()
VerifyBundleHashes()
VerifyBundleCounts()
VerifyCrossFileIdentity()
VerifyProfiles()
VerifyReleaseStatus()
```

## 34. VBA Architecture

Recommended modules:

```text
modExportBundleController
modExportBundleBuilder
modExportBundleValidator
modExportBundleManifest
modExportBundleCommit
modExportBundleHash
modExportRegistry
```

## 35. Public VBA Contract

```text
CreateExportBundle(PackageID, BundleProfileID) As BundleResult
ValidateExportBundle(BundleID) As BundleValidationResult
CommitExportBundle(BundleID) As BundleResult
```

## 36. BundleResult

Minimum fields:

```text
Success
BundleID
BundlePath
BundleStatus
FileCount
TotalSize
BundleHash
ErrorCode
ErrorMessage
```

`BundleHash` may represent the committed Bundle verification record; individual file hashes remain in the Manifest/Registry.

## 37. Error Codes

```text
EXP-BND-001 BUNDLE_CREATE_ERROR
EXP-BND-002 BUNDLE_INCOMPLETE
EXP-BND-003 BUNDLE_FILE_MISSING
EXP-BND-004 BUNDLE_FILE_SIZE_MISMATCH
EXP-BND-005 BUNDLE_RECORD_COUNT_MISMATCH
EXP-BND-006 BUNDLE_HASH_MISMATCH
EXP-BND-007 BUNDLE_PACKAGE_MISMATCH
EXP-BND-008 BUNDLE_VERSION_MISMATCH
EXP-BND-009 BUNDLE_PROFILE_MISMATCH
EXP-BND-010 BUNDLE_SCHEMA_MISMATCH
EXP-BND-011 BUNDLE_RELEASE_BLOCKED
EXP-BND-012 BUNDLE_COMMIT_ERROR
EXP-BND-013 BUNDLE_VERIFICATION_ERROR
EXP-BND-014 BUNDLE_ALREADY_EXISTS
EXP-BND-015 BUNDLE_MODIFIED
```

## 38. Acceptance Criteria

TB-037 is accepted when:

```text
RESULT.csv generated
DATASET.csv generated
AUDIT.csv generated
MANIFEST.csv generated
All files belong to same Package
Same PackageVersion
Correct ProfileID
Correct SchemaVersion
Correct RecordCount
Correct FileSize
Correct SHA-256
Cross-file consistency verified
Final Bundle committed atomically
Bundle Audit Event generated
No analytical recalculation performed
```

## 39. Freeze Decisions

| ID | Decision |
|---|---|
| D-781 | Final Export Bundle contains RESULT, DATASET, AUDIT and MANIFEST CSV files. |
| D-782 | BundleID is independent from PackageID. |
| D-783 | Each exported file has an independent ExportID. |
| D-784 | MANIFEST is the authoritative index of Bundle files. |
| D-785 | SHA-256 is the MVP file-integrity algorithm. |
| D-786 | Hash is calculated from the final file bytes after verification. |
| D-787 | Manifest does not self-reference its own hash. |
| D-788 | All Final Bundle files must belong to the same PackageID. |
| D-789 | All Final Bundle files must use the same PackageVersion. |
| D-790 | Final RESULT.csv requires the Release Gate to be passed. |
| D-791 | Dataset and Audit exports remain traceable to the same Released Package. |
| D-792 | Bundle creation uses temporary-file/temporary-directory transaction semantics. |
| D-793 | Partial Bundles cannot be committed as Final Bundles. |
| D-794 | Existing Final Bundles are never silently overwritten. |
| D-795 | Re-export creates a new BundleID. |
| D-796 | Previous Bundles are retained. |
| D-797 | Bundle validation includes cross-file identity checks. |
| D-798 | Bundle validation includes hash and record-count checks. |
| D-799 | Bundle creation never recalculates analytical Results. |
| D-800 | Excel Worksheet presentation is not the source of Final Export data. |
| D-801 | Export output is independent of Windows/Excel regional settings. |
| D-802 | All rules apply only to exported TXT-file tensile-test analysis. |

**Status: Approved / Frozen — TB-037.**
