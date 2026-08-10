# TB-033 — ISO 6892-1 Result Export Schema & Field-Level Data Contract Specification

**Status:** Approved / Frozen  
**Parent:** TB-032  
**Scope:** Exported TXT-file tensile-test analysis only  
**Platform:** Excel 2019 VBA Add-in  
**UI:** Excel Ribbon — English / LTR

## 1. Purpose

Defines the field-level contract for Released Result Package and machine-readable exports. Every exported field must exist in the approved Field Dictionary and have an explicit type, requirement state, unit where applicable, source, description and validation rule.

## 2. Core Schema

```text
Analysis Engine
      ↓
Released Result Package
      ↓
TB-033 Core Schema
      ↓
Export Profile
   ↙      ↓       ↘
 CSV    Excel    Audit/Dataset
```

## 3. Field Definition

Every field is defined by:

```text
FieldID
FieldName
DataType
Required
Unit
Source
Description
ValidationRule
Nullable
ExportOrder
```

## 4. Data Types

```text
STRING
INTEGER
DECIMAL
BOOLEAN
DATETIME
ENUM
HASH
IDENTIFIER
```

## 5. Requirement States

```text
MANDATORY
OPTIONAL
CONDITIONAL
```

## 6. Package Identity Fields

```text
PackageID             IDENTIFIER  MANDATORY
PackageVersion        INTEGER     MANDATORY
PackageStatus         ENUM        MANDATORY
CreationDateTime      DATETIME    MANDATORY
LastModifiedDateTime  DATETIME    MANDATORY
AnalysisVersion       STRING      MANDATORY
Standard              ENUM/STRING MANDATORY
Method                STRING      MANDATORY
```

Recommended PackageID:

```text
MTDMS-YYYY-NNNNNN
```

## 7. Package Status

```text
DRAFT
ANALYZED
REVIEWED
VALIDATED
RELEASED
REVOKED
BLOCKED
```

## 8. Source Fields

```text
SourceFileName       STRING      MANDATORY
SourceFilePath       STRING      OPTIONAL
SourceFileExtension  STRING      MANDATORY
SourceFileSize       INTEGER     OPTIONAL
SourceFileHash       HASH        MANDATORY
ImportDateTime       DATETIME    MANDATORY
ImportUser           STRING      MANDATORY
```

The original TXT file remains immutable.

## 9. Test Identification Fields

```text
TestID       IDENTIFIER  MANDATORY
SpecimenID   IDENTIFIER  MANDATORY
BatchID      IDENTIFIER  OPTIONAL
SampleID     IDENTIFIER  OPTIONAL
TestDate     DATETIME    MANDATORY
Operator     STRING      MANDATORY
MachineID    STRING      OPTIONAL
TestType     ENUM        MANDATORY
```

For the MVP:

```text
TestType = TENSILE
```

## 10. Material Fields

```text
MaterialID             IDENTIFIER  MANDATORY
MaterialName           STRING      MANDATORY
MaterialGrade          STRING      OPTIONAL
MaterialSpecification  STRING      OPTIONAL
MaterialLibraryVersion STRING      CONDITIONAL
```

Reference properties are distinct from measured Results:

```text
ReferenceYoungModulus
ReferenceYieldStrength
ReferenceUTS
ReferenceElongation
```

## 11. Geometry Fields

```text
SpecimenType             ENUM       MANDATORY
CrossSectionType         ENUM       MANDATORY
Width                    DECIMAL    CONDITIONAL  mm
Thickness                DECIMAL    CONDITIONAL  mm
Diameter                 DECIMAL    CONDITIONAL  mm
AreaInput                DECIMAL    MANDATORY    mm²
AreaCalculated           DECIMAL    MANDATORY    mm²
AreaUsed                 DECIMAL    MANDATORY    mm²
AreaUnit                 STRING     MANDATORY
AreaCalculationMethod    STRING     MANDATORY
GaugeLength              DECIMAL    MANDATORY    mm
SecondaryGaugeLength     DECIMAL    CONDITIONAL  mm
```

`AreaUsed` is authoritative for stress calculation.

## 12. Test Conditions

```text
TestTemperature          DECIMAL    OPTIONAL     °C
StrainRate               DECIMAL    OPTIONAL     1/s
CrossheadSpeed           DECIMAL    OPTIONAL     mm/min
ControlMode              ENUM       OPTIONAL
ExtensometerUsed         BOOLEAN    MANDATORY
ExtensometerGaugeLength  DECIMAL    CONDITIONAL  mm
```

## 13. Analysis Configuration

```text
AnalysisVersion
MethodVersion
StrainSourceMethod
YoungModulusMethod
YieldMethod
Rp02Method
RmMethod
FractureMethod
ElongationMethod
GraphCorrectionMethod
```

All are mandatory for a released analysis.

## 14. Event Schema

Each Event contains:

```text
EventID
EventType
Index
Time
Force
Displacement
Stress
Strain
DetectionMethod
DetectionStatus
AutomaticValue
FinalValue
OverrideStatus
```

## 15. Event Types

```text
TEST_START
EXTENSOMETER_RELEASE
YIELD
RP02
RM
FRACTURE
```

## 16. Event Index Contract

```text
0 <= Index < DatasetLength
```

An invalid Dataset index is `CRITICAL` and `BLOCKING`.

## 17. Event Detection Method

```text
AUTOMATIC
OPERATOR
HYBRID
```

Automatic/Operator disagreement is not itself an Error. The final value must pass all active validation rules.

## 18. Mechanical Result Fields

```text
YoungModulus       DECIMAL  GPa  MANDATORY
YieldStrength      DECIMAL  MPa  CONDITIONAL
Rp0.2              DECIMAL  MPa  CONDITIONAL
Rm                 DECIMAL  MPa  MANDATORY
MaximumForce       DECIMAL  N    MANDATORY
FractureForce      DECIMAL  N    CONDITIONAL
```

## 19. Result Metadata

Each Result must be traceable through:

```text
ResultID
ResultName
Value
Unit
Source
CalculationMethod
CalculationVersion
Status
```

## 20. Rp0.2 Fields

```text
Rp0.2
Rp0.2Unit
Rp0.2Index
Rp0.2Strain
Rp0.2Method
```

The Rp0.2 Result must be traceable to its Dataset/Event boundary.

## 21. Rm Fields

```text
Rm
RmUnit
RmIndex
RmForce
RmStrain
```

Rm represents the maximum engineering stress according to the active ISO 6892-1 Methodology RuleSet.

## 22. Fracture Fields

```text
FractureIndex
FractureTime
FractureForce
FractureStress
FractureStrain
```

## 23. Elongation Fields

```text
InitialGaugeLength
FinalGaugeLength
ElongationAfterFracture
ElongationUnit
ElongationMethod
MeasurementSource
```

Elongation is based on the approved gauge-length measurement workflow.

## 24. Strain Source Fields

```text
StrainSourceMethod
ExtensometerReleaseIndex
StrainSourceBeforeRelease
StrainSourceAfterRelease
```

Permitted source values:

```text
EXTENSOMETER
CROSSHEAD
```

## 25. Curve Dataset Fields

```text
Index              INTEGER
Time               DECIMAL       s
Force              DECIMAL       N
Displacement       DECIMAL       mm
StrainSource       ENUM
EngineeringStrain  DECIMAL       %
EngineeringStress  DECIMAL       MPa
CorrectedStrain    DECIMAL       %
```

## 26. Raw vs Corrected Strain

```text
EngineeringStrain
CorrectedStrain
```

are separate fields. CorrectedStrain is presentation/graph data and never overwrites the analytical source.

## 27. Graph Correction Metadata

```text
CorrectionApplied
CorrectionMethod
ReferenceYoungModulus
SecondaryGaugeLength
CorrectionVersion
```

## 28. Validation Fields

```text
ValidationRunID
ValidationVersion
ValidationStatus
CriticalCount
WarningCount
InfoCount
BlockingCount
```

ValidationStatus:

```text
VALID
VALID_WITH_WARNING
INVALID
PENDING
```

## 29. Release Fields

```text
ReleaseGateStatus
ReleaseEligible
ReleaseDecision
ReleaseDateTime
ReleasedBy
ReleaseSnapshotID
```

ReleaseGateStatus:

```text
OPEN
BLOCKED
```

ReleaseDecision:

```text
RELEASED
NOT_RELEASED
REVOKED
```

## 30. Provenance Fields

```text
SourceFileHash
AnalysisVersion
MethodVersion
CalculationRunID
ValidationRunID
ReviewSessionID
ReleaseSnapshotID
```

## 31. Audit Fields

```text
AuditRecordID
AuditTimestamp
User
Action
ObjectType
ObjectID
OldValue
NewValue
Reason
```

## 32. Override Fields

```text
OverrideID
ReviewSessionID
ObjectType
ObjectID
AutomaticValue
OperatorValue
Reason
Operator
Timestamp
Status
```

## 33. Export Manifest

```text
ExportID
ExportFormat
ExportVersion
GeneratedDateTime
GeneratedBy
PackageID
PackageVersion
ExportHash
```

## 34. CSV Result Profile

The MVP Result CSV contains:

```text
PackageID
PackageVersion
TestID
SpecimenID
MaterialID
Standard
Method
TestDate
Area
AreaUnit
GaugeLength
GaugeLengthUnit
YoungModulus
YoungModulusUnit
YieldStrength
YieldStrengthUnit
Rp0.2
Rp0.2Unit
Rm
RmUnit
ElongationAfterFracture
ElongationUnit
ValidationStatus
ReleaseStatus
```

## 35. Dataset Export Profile

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

## 36. Audit Export Profile

When enabled:

```text
AuditRecordID
PackageID
PackageVersion
ReviewSessionID
OverrideID
Timestamp
Operator
Action
ObjectType
ObjectID
OldValue
NewValue
Reason
```

## 37. CSV Header Contract

MVP Result CSV header:

```text
PackageID,PackageVersion,TestID,SpecimenID,MaterialID,Standard,Method,TestDate,Area,AreaUnit,GaugeLength,GaugeLengthUnit,YoungModulus,YoungModulusUnit,YieldStrength,YieldStrengthUnit,Rp0.2,Rp0.2Unit,Rm,RmUnit,ElongationAfterFracture,ElongationUnit,ValidationStatus,ReleaseStatus
```

## 38. Encoding and Decimal Convention

MVP machine-readable CSV:

```text
Encoding = UTF-8
DecimalSeparator = .
Delimiter = ,
```

Localized Excel CSV output is a separate Export Profile and must not alter the Core Schema.

## 39. Missing Value Contract

Missing values must not be represented by fabricated numbers such as `0`, `-1` or `9999`.

Permitted representation is determined by Export Profile, including:

```text
NOT_AVAILABLE
```

or an empty field where explicitly specified.

## 40. NOT_AVAILABLE vs NOT_APPLICABLE

```text
NOT_AVAILABLE = expected information is unavailable
NOT_APPLICABLE = field/result does not apply to this Method/Test
```

They must not be conflated.

## 41. Field-Level Validation

Every Mandatory field must satisfy:

```text
Exists
CorrectType
CorrectUnit
ValidRange
ValidSource
```

## 42. Cross-Field Validation

Examples:

```text
TestStart < ExtensometerReleaseIndex
Rp0.2Index < RmIndex
RmIndex < FractureIndex
AreaUsed > 0
GaugeLength > 0
```

where applicable under the active Methodology RuleSet.

## 43. Result-to-Event Integrity

Results such as Rm and Rp0.2 must remain traceable to their Event/Dataset boundaries. A Result with no valid source boundary is a traceability error.

## 44. Result-to-Geometry Integrity

Engineering Stress must be reproducible from Force and AreaUsed within the tolerance defined by the active Calculation RuleSet.

## 45. Schema Version

Example:

```text
MTDMS-RESULT-SCHEMA-1.0
```

Semantic or breaking changes require a new Schema Version.

## 46. Change Categories

```text
ADDITIVE
BREAKING
SEMANTIC
```

Adding an Optional field may be additive. Removing/changing a field Type or changing its meaning is breaking/semantic and requires versioning.

## 47. Core Schema vs Export Profile

Core Schema contains the complete approved Result model. Export Profiles select fields for CSV, Excel, Audit and Dataset outputs.

## 48. Forbidden Public Export Fields

Without an explicit profile, public Result Export must exclude:

```text
Internal Debug State
Temporary Markers
Temporary Search Windows
Internal VBA Object References
Memory Addresses
Temporary Calculation Buffers
```

## 49. Final Result Export Rule

Only:

```text
ReleaseStatus = RELEASED
```

may be exported as a Final Result.

Blocked/review packages may only be exported using explicit Draft/Review/Diagnostic profiles.

## 50. Export Naming Contract

```text
{PackageID}_{ExportType}.{Extension}
```

Examples:

```text
MTDMS-2026-000184_RESULT.csv
MTDMS-2026-000184_DATASET.csv
MTDMS-2026-000184_AUDIT.csv
```

## 51. Export Integrity

Every generated Export may be hashed and recorded through `ExportHash`. A later hash mismatch identifies external modification.

## 52. Field Dictionary Requirement

Every future exported field must first be defined in the Field Dictionary and then referenced by an approved Export Profile.

## 53. Single Source of Truth

```text
Result Package
      ↓
CSV / Excel / Report / Dataset
```

No Export Generator independently recalculates Results.

## 54. Freeze Decisions

| ID | Decision |
|---|---|
| D-693 | Every exported field must exist in the approved Field Dictionary. |
| D-694 | Every field has an explicit Data Type. |
| D-695 | Every numeric Result has an explicit Unit where applicable. |
| D-696 | Mandatory, Optional and Conditional fields are explicitly distinguished. |
| D-697 | PackageID is mandatory in every Result Export. |
| D-698 | PackageVersion is mandatory in every Result Export. |
| D-699 | SourceFileHash is mandatory for released packages. |
| D-700 | AreaUsed is the authoritative area for stress calculation. |
| D-701 | Raw and Corrected Strain are separate fields. |
| D-702 | Automatic and Final Event values are retained where Override is applicable. |
| D-703 | Event indexes must reference valid Dataset positions. |
| D-704 | Result values must remain traceable to their source Event/Dataset state. |
| D-705 | Display rounding must never feed back into calculations. |
| D-706 | Missing and Not Applicable are distinct states. |
| D-707 | Fabricated numeric values are prohibited for missing data. |
| D-708 | CSV machine-readable decimal separator is `.`. |
| D-709 | CSV machine-readable encoding is UTF-8 for the MVP. |
| D-710 | Core Schema is independent from Export Profiles. |
| D-711 | Report generation consumes the Result Package and does not recalculate Results. |
| D-712 | Final Result Export requires `ReleaseStatus = RELEASED`. |
| D-713 | Blocked packages cannot be exported as Final Results. |
| D-714 | Export files are auditable and hashable. |
| D-715 | Schema semantic or breaking changes require a new Schema Version. |
| D-716 | Internal debug and temporary calculation data are excluded from public Result Export. |
| D-717 | All rules apply only to exported TXT-file tensile-test analysis. |

**Status: Approved / Frozen — TB-033.**
