# TB-035 — ISO 6892-1 Dataset Export Implementation & Excel 2019 VBA Streaming Specification

**Status:** Approved / Frozen  
**Parent:** TB-034  
**Scope:** Exported TXT-file tensile-test analysis only  
**Platform:** Excel 2019 VBA Add-in

## 1. Purpose

Defines the implementation contract for exporting the validated Dataset as a machine-readable CSV from Excel 2019 VBA. The Dataset Export reads only from the Released Dataset contained in the Result Package and does not recalculate analytical Results.

## 2. Dataset Export Flow

```text
Imported TXT
    ↓
Normalized Dataset
    ↓
Validated Dataset
    ↓
Released Result Package
    ↓
Dataset Export
```

## 3. MVP Header

```text
Index,Time,Force,Displacement,StrainSource,EngineeringStrain,EngineeringStress,CorrectedStrain
```

Exactly eight fields are defined for the MVP Dataset profile.

## 4. Field Contract

| Field | Type | Unit | Rule |
|---|---|---|---|
| Index | INTEGER | — | Unique, ascending |
| Time | DECIMAL | s | Non-decreasing |
| Force | DECIMAL | N | Normalized source value |
| Displacement | DECIMAL | mm | Validated dataset value |
| StrainSource | ENUM | — | EXTENSOMETER/CROSSHEAD |
| EngineeringStrain | DECIMAL | % | Analysis dataset value |
| EngineeringStress | DECIMAL | MPa | Analysis dataset value |
| CorrectedStrain | DECIMAL | % | Separate presentation/correction field |

## 5. Array Alignment

All Dataset arrays must have identical length:

```text
Index[]
Time[]
Force[]
Displacement[]
StrainSource[]
EngineeringStrain[]
EngineeringStress[]
CorrectedStrain[]
```

For every valid point `i`, all required fields must refer to the same physical test point.

## 6. Index Rules

```text
Index is INTEGER
Index is UNIQUE
Index is ASCENDING
```

MVP expects continuous indexes unless an approved Dataset RuleSet explicitly permits gaps.

## 7. Time Rules

```text
Time(i+1) >= Time(i)
```

The Exporter must not generate or interpolate new timestamps.

## 8. Force

Contractual export unit is `N`. Any source-unit normalization belongs to the analysis/normalization layer and is not repeated by the CSV Writer.

## 9. Displacement

Contractual export unit is `mm`. The exporter serializes the validated Dataset value without silently transforming it.

## 10. Strain Source

Permitted values:

```text
EXTENSOMETER
CROSSHEAD
```

The transition boundary must remain traceable to the Extensometer Release rules.

## 11. Engineering Strain

Contractual export unit is `%`. The exporter does not calculate strain from displacement.

## 12. Engineering Stress

Contractual export unit is `MPa`. The exporter does not recalculate stress from Force and Area.

## 13. Corrected Strain

`CorrectedStrain` is independent of `EngineeringStrain` and must never overwrite the analytical strain source.

If correction is not applicable, the selected Export Profile determines whether the value is `NOT_APPLICABLE` or another explicitly defined representation. The exporter must not guess.

## 14. Rm and Fracture Boundaries

Dataset Export does not truncate at Rm. Points between Rm and fracture remain available when present in the Released Dataset.

Post-fracture data is exported only when present in the Released Dataset and permitted by the selected Export Profile.

## 15. Point Integrity

Every required Dataset point must contain all mandatory fields. Missing values may be emitted only when the Field Dictionary/Profile explicitly allows them.

Fabricated numeric placeholders such as `0`, `-1` or `9999` are prohibited.

## 16. Streaming Requirement

For large Dataset files, implementation should use streaming row-by-row serialization:

```text
Read Point
  ↓
Serialize Point
  ↓
Write Row
  ↓
Read Next Point
```

The entire Dataset must not be assembled into one large VBA String unless explicitly justified by a profile-specific limit.

## 17. VBA Module Separation

Recommended responsibilities:

```text
DatasetProvider
DatasetSerializer
CsvWriter
ExportValidator
ExportManifest
HashProvider
```

The Dataset Provider obtains data from the Result Package. The Serializer converts values to contractual text. The CSV Writer writes bytes/records. No component may bypass the Result Package to read Worksheet presentation cells.

## 18. Worksheet Independence

Dataset Export must not depend on fixed worksheet addresses such as `Sheet1!A:A` as the authoritative source.

Worksheets are presentation/review/report surfaces, not the Result Package source of truth.

## 19. Deterministic Ordering

Rows must be written in ascending Dataset Index order. Dictionary, Collection or Worksheet enumeration order must never determine output order.

## 20. CSV Serialization

MVP rules:

```text
Delimiter = ,
DecimalSeparator = .
Encoding = UTF-8
UTF-8 BOM = enabled by default
```

Fields containing comma, quote, CR or LF must be quoted according to CSV rules. Embedded quotes are doubled.

## 21. Temporary File Transaction

Dataset export must use:

```text
Create .tmp
    ↓
Write Header
    ↓
Write Dataset Rows
    ↓
Flush / Close
    ↓
Verify
    ↓
Hash
    ↓
Rename to Final
```

A partial file must never be accepted as a Final Dataset Export.

## 22. Row Count Verification

After writing:

```text
ExpectedRowCount = DatasetLength
ActualRowCount = CSV data rows
```

These values must match.

## 23. Column Count Verification

```text
ExpectedColumns = 8
ActualColumns = 8
```

Any mismatch is a blocking export error.

## 24. Dataset Verification

Minimum checks:

```text
FileExists
FileSize > 0
HeaderValid
ColumnCountValid
RowCountValid
IndexValid
TimeOrderValid
EncodingValid
```

## 25. Export Hash

Hash is calculated only after successful file verification and persisted in the Export Manifest.

## 26. Audit Events

Minimum events:

```text
DATASET_EXPORT_STARTED
DATASET_EXPORT_VALIDATED
DATASET_EXPORT_CREATED
DATASET_EXPORT_VERIFIED
DATASET_EXPORT_COMPLETED
DATASET_EXPORT_FAILED
```

## 27. API Contract

Recommended public VBA interface:

```text
ExportDataset(PackageID, ProfileID) As ExportResult
```

Supporting operations:

```text
BeginDatasetExport(...)
WriteDatasetHeader(...)
WriteDatasetPoint(...)
FinalizeDatasetExport(...)
VerifyDatasetExport(...)
```

## 28. ExportResult

Minimum result structure:

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

## 29. Error Codes

```text
EXP-DATA-001 DATASET_COLUMN_COUNT_ERROR
EXP-DATA-002 DATASET_TIME_ORDER_ERROR
EXP-DATA-003 DATASET_INDEX_ERROR
EXP-DATA-004 DATASET_ARRAY_LENGTH_ERROR
EXP-DATA-005 DATASET_POINT_INVALID
EXP-DATA-006 DATASET_WRITE_ERROR
EXP-DATA-007 DATASET_ROW_COUNT_ERROR
EXP-DATA-008 DATASET_SOURCE_BOUNDARY_ERROR
EXP-DATA-009 DATASET_VERIFICATION_ERROR
```

## 30. Failure Handling

Any critical failure must result in:

```text
Final Dataset Export = FAILED
```

The incomplete temporary file must not be registered as a Final Export.

## 31. No Silent Transformation

The exporter must not silently alter Force, Time, Displacement, Stress, Strain or StrainSource. Any permitted unit conversion or serialization conversion must be explicitly defined by the Export Profile.

## 32. Reproducibility

The same:

```text
PackageVersion
SchemaVersion
ExportProfileVersion
```

must produce deterministic Dataset ordering and serialization.

## 33. Dataset Immutability

Export must not modify:

```text
Result Package
Raw Dataset
Normalized Dataset
Corrected Dataset
Review Data
Audit Data
```

## 34. Retry

A failed export retries from the same Released Package. Analysis is not rerun merely because file writing failed.

## 35. Freeze Decisions

| ID | Decision |
|---|---|
| D-745 | Dataset Export reads only from the Released Dataset contained in the Result Package. |
| D-746 | Dataset Export never recalculates Results. |
| D-747 | Dataset Header contains exactly 8 MVP fields. |
| D-748 | All Dataset arrays must have identical length. |
| D-749 | Dataset Index is deterministic and ascending. |
| D-750 | Dataset Time must be non-decreasing. |
| D-751 | Force export unit is N. |
| D-752 | Displacement export unit is mm. |
| D-753 | Engineering Stress export unit is MPa. |
| D-754 | Engineering Strain export unit is %. |
| D-755 | StrainSource is explicitly exported. |
| D-756 | CorrectedStrain is separate from EngineeringStrain. |
| D-757 | Dataset Export uses temporary-file transaction semantics. |
| D-758 | Partial Dataset files cannot be accepted as Final Export. |
| D-759 | Dataset Row Count must equal expected Dataset Length. |
| D-760 | Dataset Export is deterministic. |
| D-761 | Dataset Export is hashable and auditable. |
| D-762 | All rules apply only to exported TXT-file tensile-test analysis. |

**Status: Approved / Frozen — TB-035.**
