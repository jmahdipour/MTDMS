# TB-034 — ISO 6892-1 CSV Result Export Implementation Contract & Excel 2019 VBA Serialization Specification

**Status:** Approved / Frozen  
**Parent:** TB-033  
**Scope:** Exported TXT-file tensile-test analysis only  
**Platform:** Excel 2019 VBA Add-in  
**UI:** Excel Ribbon — English / LTR

## 1. Purpose

Defines the implementation contract for generating machine-readable CSV exports from the released Result Package. TB-033 defines the field-level data contract; TB-034 defines serialization, CSV writing, validation, file integrity and Excel 2019 VBA implementation rules.

## 2. Single Source of Truth

Final export source is exclusively the **Released Result Package**.

```text
TXT → Import → Analysis → Review → Validation → Release Package → CSV
```

The CSV writer must never independently recalculate analytical results.

## 3. Export Types

MVP profiles:

```text
RESULT
DATASET
AUDIT
```

Example names:

```text
MTDMS-2026-000184_RESULT.csv
MTDMS-2026-000184_DATASET.csv
MTDMS-2026-000184_AUDIT.csv
```

## 4. Final Export Eligibility

A Final Result export requires:

```text
PackageStatus = RELEASED
ReleaseEligible = TRUE
ValidationStatus = VALID
BlockingCount = 0
```

Otherwise the export is blocked.

## 5. MVP Result Export Profile

```text
ProfileID = ISO6892_RESULT_CSV
ProfileVersion = 1.0
Format = CSV
Encoding = UTF-8
Delimiter = ,
DecimalSeparator = .
```

## 6. Header Contract

The MVP Result CSV header is fixed:

```text
PackageID,PackageVersion,TestID,SpecimenID,MaterialID,Standard,Method,TestDate,Area,AreaUnit,GaugeLength,GaugeLengthUnit,YoungModulus,YoungModulusUnit,YieldStrength,YieldStrengthUnit,Rp0.2,Rp0.2Unit,Rm,RmUnit,ElongationAfterFracture,ElongationUnit,ValidationStatus,ReleaseStatus
```

Header must not be translated or altered by regional settings.

## 7. Field Mapping

| CSV Field | Result Package Source |
|---|---|
| PackageID | Package.Identity.PackageID |
| PackageVersion | Package.Identity.PackageVersion |
| TestID | Test.TestID |
| SpecimenID | Test.SpecimenID |
| MaterialID | Material.MaterialID |
| Standard | Analysis.Standard |
| Method | Analysis.Method |
| TestDate | Test.TestDate |
| Area | Geometry.AreaUsed |
| AreaUnit | Geometry.AreaUnit |
| GaugeLength | Geometry.GaugeLength |
| GaugeLengthUnit | `mm` |
| YoungModulus | Results.YoungModulus |
| YoungModulusUnit | `GPa` |
| YieldStrength | Results.YieldStrength |
| YieldStrengthUnit | `MPa` |
| Rp0.2 | Results.Rp0.2 |
| Rp0.2Unit | `MPa` |
| Rm | Results.Rm |
| RmUnit | `MPa` |
| ElongationAfterFracture | Results.ElongationAfterFracture |
| ElongationUnit | `%` |
| ValidationStatus | Validation.ValidationStatus |
| ReleaseStatus | Release.ReleaseDecision |

## 8. No Recalculation Rule

The writer performs only:

```text
Read → Validate → Serialize → Write
```

It must not calculate stress, Rp0.2, Rm, Young's modulus or elongation.

## 9. VBA Module Architecture

Recommended modules:

```text
modExportController
modCsvWriter
modCsvSerializer
modCsvEscaping
modExportProfile
modFieldDictionary
modExportValidator
modExportManifest
modUtf8Writer
modHash
```

## 10. Separation of Concerns

Analysis, Result Package, serialization and file writing are separate layers.

Worksheet layout must not be the source of exported Results.

## 11. Serialization Data Types

Supported types:

```text
STRING
INTEGER
DECIMAL
BOOLEAN
DATETIME
ENUM
IDENTIFIER
HASH
```

## 12. Decimal Serialization

Machine-readable decimal separator is always `.` regardless of Windows/Excel locale.

Display precision must not overwrite analytical precision.

## 13. Scientific Notation

MVP scientific notation is disabled unless explicitly enabled by an Export Profile.

## 14. Boolean Serialization

```text
TRUE
FALSE
```

## 15. DateTime Serialization

Use locale-independent format:

```text
YYYY-MM-DDTHH:MM:SS
```

TestDate must come from the Result Package, not the export timestamp.

## 16. Missing Values

Missing values must never be represented by fabricated numbers such as `0`, `-1` or `9999`.

Permitted profile tokens include:

```text
NOT_AVAILABLE
NOT_APPLICABLE
```

These states must remain distinct.

## 17. CSV Escaping

Fields containing comma, quote, CR or LF must be quoted according to CSV rules. Embedded quotes are doubled.

Example:

```text
"Grade ""A"""
```

## 18. Row Integrity

Every row must contain exactly the same number of fields as the header. For the MVP Result profile this is 25 fields.

## 19. Column Order

Column order comes exclusively from `ExportProfile.FieldList`; it must not depend on Dictionary, Collection or Worksheet ordering.

## 20. Field Dictionary

Every exported field must have:

```text
FieldID
FieldName
DataType
Unit
Required
SourcePath
Serializer
ValidationRule
```

## 21. Schema Compatibility

`Package.SchemaVersion` must be compatible with the selected Export Profile.

Mismatch blocks export.

## 22. Required Field Validation

Every mandatory field must satisfy:

```text
Exists
CorrectType
CorrectUnit
ValidRange
ValidSource
```

## 23. Unit Validation

MVP Result units include:

```text
Area = mm²
GaugeLength = mm
YoungModulus = GPa
YieldStrength = MPa
Rp0.2 = MPa
Rm = MPa
ElongationAfterFracture = %
```

## 24. Result Validation

Released results must satisfy the active validation contract. Invalid or blocking results cannot be exported as Final Results.

## 25. Source Traceability

Released packages require `SourceFileHash`. Missing source traceability blocks Final Export.

## 26. File Naming

```text
{PackageID}_RESULT.csv
{PackageID}_DATASET.csv
{PackageID}_AUDIT.csv
```

## 27. Existing File Protection

MVP must not overwrite an existing Final Export automatically. Replacement requires explicit authorization and Audit logging.

## 28. Temporary File Strategy

Final files must be produced transactionally:

```text
Write .tmp → Verify → Hash → Rename to final
```

A partial `.tmp` file must never be accepted as a Final Export.

## 29. Atomic Export

If a critical write or validation step fails, the final target file must not be created or replaced.

## 30. Post-Write Verification

Verify at minimum:

```text
FileExists
FileSize > 0
HeaderValid
ColumnCountValid
RowCountValid
EncodingValid
```

## 31. Export Hash

After successful verification, calculate `ExportHash` and persist it in the Export Manifest.

## 32. Export Manifest

Minimum fields:

```text
ExportID
PackageID
PackageVersion
ExportFormat
ExportVersion
GeneratedDateTime
GeneratedBy
ExportHash
```

## 33. Export Audit

Record successful and failed operations, including:

```text
EXPORT_STARTED
EXPORT_VALIDATED
EXPORT_CREATED
EXPORT_VERIFIED
EXPORT_COMPLETED
EXPORT_FAILED
```

## 34. Error Codes

Minimum codes:

```text
EXP-001 FINAL_EXPORT_BLOCKED
EXP-002 SCHEMA_VERSION_MISMATCH
EXP-003 FIELD_NOT_FOUND
EXP-004 FIELD_TYPE_ERROR
EXP-005 FIELD_UNIT_ERROR
EXP-006 REQUIRED_VALUE_MISSING
EXP-007 COLUMN_COUNT_ERROR
EXP-008 CSV_WRITE_ERROR
EXP-009 FILE_EXISTS
EXP-010 FILE_HASH_ERROR
EXP-011 SOURCE_TRACEABILITY_ERROR
EXP-012 RESULT_INVALID
EXP-013 PACKAGE_NOT_RELEASED
EXP-014 EXPORT_VERIFICATION_FAILED
```

## 35. Error Boundary

Internal VBA runtime errors must be converted into controlled application error records containing ErrorCode, message, PackageID/FieldID where applicable, timestamp and severity.

## 36. UTF-8

MVP requires UTF-8 CSV independent of Windows code page and Excel regional settings. UTF-8 with BOM is the default compatibility profile for Excel 2019.

## 37. Dataset Export

Dataset export contains:

```text
Index
Time
Force
Displacement
StrainSource
EngineeringStrain
EngineeringStress
CorrectedStrain
```

Dataset rows must be deterministic and ordered by ascending Index.

## 38. Dataset Integrity

At minimum validate:

```text
Index Unique
Index Continuous
Time Non-decreasing
```

unless an approved Dataset RuleSet explicitly permits gaps.

## 39. Internal vs Export Units

Unit conversion between the internal calculation representation and the contractual export unit is permitted only as a serialization rule. It must not introduce a new analytical calculation.

## 40. Rounding

Export precision is controlled by Export Profile. Report display rounding must never feed back into calculations.

## 41. Export Reproducibility

Same PackageVersion, SchemaVersion and ExportProfileVersion must produce deterministic field ordering and serialization.

## 42. No Data Mutation

Export must not modify Result Package, raw dataset, corrected dataset, review data or audit data.

## 43. Retry

A failed export retries from the same Released Package; analysis is not rerun merely because file writing failed.

## 44. Export Location

Default:

```text
<PackageFolder>\Exports\
```

## 45. Public vs Diagnostic Export

Final Result exports are available only to Released Packages. Draft/Review/Diagnostic exports require explicit profiles and must never be confused with Final Results.

## 46. Version Independence

The following versions remain independent:

```text
AnalysisVersion
SchemaVersion
ExportProfileVersion
```

## 47. Public Export Exclusions

Unless an explicit diagnostic profile exists, exclude:

```text
Internal Debug State
Temporary Markers
Temporary Search Windows
Internal VBA Object References
Memory Addresses
Temporary Calculation Buffers
```

## 48. VBA Public Contract

Recommended interface:

```text
ExportResultPackage(PackageID, ProfileID) As ExportResult
ExportDataset(PackageID, ProfileID) As ExportResult
```

`ExportResult` contains:

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

## 49. Transactional Export

Logical transaction:

```text
BEGIN
Validate
Serialize
Write Temp
Verify
Hash
Commit Manifest
END
```

Any Critical Failure results in rollback and no Final Export commitment.

## 50. Freeze Decisions

| ID | Decision |
|---|---|
| D-718 | CSV Export reads only from the Released Result Package. |
| D-719 | CSV Writer never performs analytical calculations. |
| D-720 | Export Profile controls field order and serialization rules. |
| D-721 | CSV machine-readable delimiter is comma. |
| D-722 | CSV machine-readable decimal separator is period. |
| D-723 | MVP CSV encoding is UTF-8. |
| D-724 | MVP UTF-8 CSV uses BOM for Excel 2019 compatibility. |
| D-725 | Header and column order are fixed by Export Profile. |
| D-726 | CSV field count must equal header field count. |
| D-727 | Missing values must never be fabricated numeric values. |
| D-728 | NOT_AVAILABLE and NOT_APPLICABLE remain distinct. |
| D-729 | Raw and Corrected Strain remain separate. |
| D-730 | Export does not mutate the Result Package. |
| D-731 | Final Export requires ReleaseStatus = RELEASED. |
| D-732 | Final Export is written through a temporary file before commit. |
| D-733 | Partial files cannot be accepted as Final Export. |
| D-734 | Existing Final Export files are not overwritten by default. |
| D-735 | Export Manifest is committed only after successful verification. |
| D-736 | Every Export receives an ExportID. |
| D-737 | Every Export can be associated with an ExportHash. |
| D-738 | Export failures generate explicit Error Codes. |
| D-739 | Export Audit records successful and failed export operations. |
| D-740 | Excel Worksheet layout is not the source of exported Results. |
| D-741 | Dataset Export uses deterministic ascending Index order. |
| D-742 | Internal calculation precision is not replaced by Report display precision. |
| D-743 | AnalysisVersion, SchemaVersion and ExportProfileVersion are independent. |
| D-744 | All rules apply only to exported TXT-file tensile-test analysis. |

**Status: Approved / Frozen — TB-034.**
