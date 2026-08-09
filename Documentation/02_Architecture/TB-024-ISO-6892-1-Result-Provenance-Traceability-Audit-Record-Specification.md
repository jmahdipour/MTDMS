# TB-024 — ISO 6892-1 Result Provenance, Traceability & Audit Record Specification

**Status:** Approved / Frozen  
**Scope:** Output TXT file analysis only  
**Parent:** TB-023  
**Platform:** Excel 2019 VBA Add-in  

## Purpose

Every final Result must be traceable and reproducible back to the source TXT Dataset. Raw, Calculated and Corrected/Presentation data remain separate and auditable.

## Provenance Layers

```text
RAW
 ↓
CALCULATED
 ↓
CORRECTED / PRESENTATION
```

## Source Identity

The analysis package records:

- SourceFileName
- SourceFilePath
- FileHash
- FileSize
- FileModifiedDate
- ImportTimestamp
- OriginalRowIndex
- SourceColumn
- OriginalValue
- OriginalUnit

Raw source files are immutable from the application's analytical perspective.

## Dataset Traceability

Every Dataset row retains `OriginalRowIndex`. Filtering, sorting and transformation must not break the mapping to the original TXT row.

Dataset transformations receive explicit versions, e.g.:

```text
RAW-V1
NORMALIZED-V1
DERIVED-V1
VALID-V1
```

## Unit Provenance

For every normalized quantity:

```text
OriginalUnit
NormalizedUnit
ConversionApplied
ConversionFactor
```

must be traceable.

## Result Provenance

Each Result has:

```text
ResultID
ResultVersion
ResultValue
ResultUnit
ResultStatus
DatasetVersion
MethodVersion
ConfigurationVersion
CalculationVersion
InputDependencies
EventDependencies
ValidationDependencies
AuditReference
```

## Result Dependency Trace

Example:

```text
Rp0.2
 ├── Stress Dataset
 ├── Strain Dataset
 ├── Young Modulus
 ├── Offset
 ├── Elastic Boundary
 └── Method
```

A Result cannot depend on hidden or unrecorded state.

## Event Provenance

The following Events are independently traceable:

```text
TestStart
ExtensometerRelease
Yield
Rp0.2
Rm
Fracture
```

Each Event records, where applicable:

```text
EventType
DatasetIndex
OriginalRowIndex
DetectionMethod
DetectionStatus
AlgorithmVersion
Threshold
SearchRegion
CandidateIndex
FinalIndex
```

Extensometer Release and Fracture remain independent Events. Yield and Rp0.2 also remain independent concepts.

## Automatic vs Operator Event Values

Operator changes never erase automatic detection. Both are preserved:

```text
AutomaticIndex
OperatorIndex
FinalIndex
```

Any override requires:

```text
OverrideID
OriginalValue
NewValue
Operator
Timestamp
Reason
```

## Strain Source Provenance

Every strain segment identifies its source:

```text
Extensometer
Crosshead
Segmented / Combined Source
```

For an Extensometer Release, the provenance records:

```text
ReleaseIndex
ReleaseOriginalRow
PreviousSource
NewSource
DetectionMethod
OverrideStatus
```

## Gauge-Length Provenance

`L0` and `L_after` are independent measurements with their own:

```text
Value
Unit
MeasurementSource
Operator
Timestamp
```

`L_after` also references the finalized Fracture Event.

## A% Provenance

Elongation after fracture remains reconstructable from:

```text
L0
L_after
FormulaVersion
UnitNormalization
FractureReference
```

A% is not stored only as an isolated numeric value.

## Graph Correction Provenance

Graph correction never overwrites the original strain Dataset:

```text
OriginalStrain
       ↓
CorrectionParameters
       ↓
CorrectedStrain
```

Correction parameters include, where applicable:

```text
ReferenceYoungModulus
SecondaryGaugeLength
ElasticRegion
CorrectionMethod
CorrectionVersion
Operator
Timestamp
```

## Validation Provenance

Each Result links to the Validation rules used by TB-023:

```text
RuleID
RuleVersion
Severity
Expected
Actual
Status
```

This distinguishes provenance from validation:

```text
Provenance = where/how the Result was produced
Validation  = whether the Result is acceptable
```

## Audit Record

Audit records describe who changed what and why:

```text
AuditID
Timestamp
OperatorID
Action
ObjectType
ObjectID
OldValue
NewValue
Trigger
Reason
RelatedResult
```

Typical Actions include:

```text
IMPORT
NORMALIZE
CALCULATE
DETECT
OVERRIDE
CORRECT
VALIDATE
RECALCULATE
REPORT
```

## Recalculation Audit

A recalculation records:

```text
Trigger
PreviousVersion
NewVersion
ChangedDependency
AffectedResults
```

Example:

```text
Trigger = EVENT_OVERRIDE
ChangedDependency = ExtensometerRelease
AffectedResults =
    EngineeringStrain
    YoungModulus
    Rp0.2
```

## Method / Configuration / Library Changes

Changes to Method, Configuration or Material Library data are audited with old value, new value, operator, timestamp, reason and affected operations/results.

Examples include:

```text
OldMethod / NewMethod
OldArea / NewArea
OldReferenceE / NewReferenceE
```

## Reproducibility

A Result must be reproducible when the same:

```text
Source File
Dataset Version
Method Version
Configuration Version
Calculation Version
Validation Rules
```

are used.

Source, Dataset and Configuration hashes may be stored for integrity checking. A Result Package may also receive a package fingerprint.

## Provenance Status

```text
COMPLETE
PARTIAL
BROKEN
```

`BROKEN` provenance prevents finalization.

## Final Result Package

```text
FinalResultPackage
├── Source
├── Dataset
├── Events
├── Calculations
├── Results
├── Corrections
├── Validations
├── QualityStatus
└── Audit
```

## Report Traceability

A Report must remain traceable to at least:

```text
ResultID
ResultVersion
TestID
SourceFile
```

A one-page report may omit detailed provenance visually, but the underlying analytical package must retain it.

## Core Rules

1. Raw Data is immutable.
2. Calculated Data is separate from Corrected Data.
3. Every Result is traceable.
4. Every Event is traceable.
5. Every Override is auditable.
6. Every Calculation has a version.
7. Every Method has a version.
8. Every Configuration has a version.
9. Every Dataset has a version.
10. No Result may depend on hidden state.

## Freeze Decisions

| ID | Decision |
|---|---|
| D-486 | Every Final Result must be traceable to the Source TXT. |
| D-487 | Raw, Calculated and Corrected/Presentation Data are separate. |
| D-488 | Raw Source is immutable. |
| D-489 | File Hash is part of Source Identity. |
| D-490 | OriginalRowIndex is retained. |
| D-491 | Source Column and Original Unit are traceable. |
| D-492 | Unit Conversion is part of Provenance. |
| D-493 | Every Result has ResultID and ResultVersion. |
| D-494 | Every Result identifies its Calculation Version. |
| D-495 | Dataset, Method, Configuration and Calculation Versions are recorded. |
| D-496 | Yield, Rp0.2, ExtensometerRelease and Fracture are independently auditable Events. |
| D-497 | Automatic and Operator Event values are both preserved. |
| D-498 | Override without OriginalValue is prohibited. |
| D-499 | L0 and L_after have independent Measurement Provenance. |
| D-500 | A% is traceable to L0 and L_after. |
| D-501 | Graph Correction cannot overwrite the Original Dataset. |
| D-502 | Correction Parameters are auditable. |
| D-503 | Validation Records are linked to Result Provenance. |
| D-504 | Audit and Provenance are separate concepts. |
| D-505 | Recalculation records its Trigger and Affected Results. |
| D-506 | Method Changes are audited. |
| D-507 | Configuration Changes are audited. |
| D-508 | Material Library Changes are auditable. |
| D-509 | Provenance uses COMPLETE/PARTIAL/BROKEN status. |
| D-510 | BROKEN Provenance prevents Finalization. |
| D-511 | Results must be reproducible without Hidden State. |
| D-512 | Reports remain traceable to ResultID/Version and Source File. |
| D-513 | Final Result Package contains Source, Dataset, Events, Calculations, Results, Corrections, Validations, QualityStatus and Audit. |

**Status: Approved / Frozen — TB-024.**
