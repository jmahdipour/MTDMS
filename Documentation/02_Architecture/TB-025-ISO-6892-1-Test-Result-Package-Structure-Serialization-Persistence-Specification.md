# TB-025 — ISO 6892-1 Test Result Package Structure, Serialization & Persistence Specification

**Status:** Approved / Frozen  
**Parent:** TB-024  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in  

## 1. Purpose

A Test Result Package is the complete, versioned, traceable representation of one test. It contains source identity, metadata, configuration, material/specimen snapshots, datasets, events, calculations, graph analysis, corrections, validation, quality status, provenance, audit and integrity information.

## 2. Logical Package Structure

```text
TestResultPackage
├── PackageIdentity
├── Source
├── TestMetadata
├── Configuration
├── Material
├── Specimen
├── RawDataset
├── NormalizedDataset
├── DerivedDataset
├── Events
├── CalculationResults
├── GraphAnalysis
├── Corrections
├── Validation
├── QualityStatus
├── Provenance
├── Audit
└── PackageIntegrity
```

## 3. Package Identity

Required identity fields:

```text
PackageID
TestID
PackageVersion
CreatedAt
ModifiedAt
SchemaVersion
ApplicationVersion
```

`PackageID`, `TestID` and `PackageVersion` are distinct concepts. `SchemaVersion` is independent of `ApplicationVersion`.

## 4. Source

```text
Source
├── FileName
├── FilePath
├── FileHash
├── FileSize
├── FileModifiedDate
├── ImportTimestamp
├── Encoding
├── Delimiter
└── SourceFormatVersion
```

The original TXT file is immutable from the analytical application's perspective.

## 5. Test Metadata

```text
TestMetadata
├── TestID
├── TestDate
├── Operator
├── Machine
├── TestType
├── Standard
├── Method
└── Notes
```

The scope remains the exported test file; no machine-control or real-time integration is defined here.

## 6. Method and Configuration

Method identity is separate from calculation version:

```text
Standard = ISO 6892-1
MethodID = ISO6892-1-Tensile
MethodVersion = 1.0
```

The effective configuration is stored as a test-time snapshot so later Settings changes cannot silently alter historical results.

```text
Configuration
├── CrossSection
├── GaugeLength
├── ForceUnit
├── DisplacementUnit
├── StrainUnit
├── YieldMethod
├── RpOffset
├── StrainSourceRule
└── GraphCorrectionRule
```

## 7. Material Snapshot

If the Material Library is used, the package stores the effective material values and library version:

```text
Material
├── MaterialID
├── MaterialName
├── Grade
├── YoungModulus
├── YieldStrength
├── TensileStrength
├── Elongation
└── LibraryVersion
```

Historical results therefore do not depend on the current state of the library.

## 8. Specimen

```text
Specimen
├── Shape
├── Width
├── Thickness
├── Diameter
├── Area
├── AreaUnit
├── GaugeLength
└── GaugeLengthUnit
```

Area calculation inputs, formula, units and calculation version remain traceable.

## 9. Dataset Layers

Three analytical layers are mandatory:

```text
RAW
NORMALIZED
DERIVED
```

### RawDataset

Closest representation to the imported TXT data. It is immutable after successful import.

### NormalizedDataset

Contains unit conversion and format normalization.

### DerivedDataset

Contains quantities such as:

```text
Stress
Strain
CorrectedStrain
TrueStress
TrueStrain
```

and other method-required derived quantities.

## 10. Dataset Versioning

Dataset transformations receive explicit versions, for example:

```text
RAW-V1
NORMALIZED-V1
DERIVED-V1
VALID-V1
```

`OriginalRowIndex` must remain available through transformations. `DatasetIndex` and `OriginalRowIndex` are separate concepts.

## 11. Events

Events are independent records:

```text
TestStart
ExtensometerRelease
Yield
Rp0.2
Rm
Fracture
```

Each Event may contain:

```text
EventID
EventType
DatasetIndex
OriginalRowIndex
DetectionMethod
DetectionVersion
AutomaticValue
OperatorValue
FinalValue
Status
AuditReference
```

Automatic and Operator values are both retained.

## 12. Calculation Results

The package may contain:

```text
Stress
YoungModulus
Yield
Rp0.2
Rm
Fracture
A%
TrueStress
TrueStrain
```

Each Result contains:

```text
ResultID
ResultName
Value
Unit
Status
MethodVersion
CalculationVersion
DatasetVersion
Dependencies
ProvenanceReference
```

## 13. Graph Analysis

Graph analysis is separated from the numerical calculation Dataset:

```text
GraphAnalysis
├── CurveDefinition
├── ElasticRegion
├── YieldMarker
├── RmMarker
├── FractureMarker
├── ReferenceLine
└── DisplaySettings
```

Display-only information such as zoom, marker visibility and display range must not alter calculation results.

## 14. Corrections

```text
Corrections
├── StrainCorrection
├── HorizontalAxisCorrection
├── EventOverrides
└── OperatorCorrections
```

A correction stores its original value, corrected value, parameters, method, version, operator, timestamp and reason.

Correction must never overwrite the Raw Dataset.

## 15. Validation and Quality Status

```text
Validation
├── Rules
├── Results
├── ErrorCount
├── WarningCount
├── CriticalCount
└── ValidationVersion
```

Quality status values:

```text
PASS
PASS_WITH_WARNING
FAIL
INCOMPLETE
```

A critical validation failure prevents Finalization.

## 16. Provenance and Audit

Provenance contains references to Source, Dataset, Events, Results, Method, Configuration, Calculation and Validation.

Audit records who changed what and why:

```text
Audit
├── AuditID
├── Timestamp
├── Operator
├── Action
├── ObjectType
├── ObjectID
├── OldValue
├── NewValue
├── Reason
└── Trigger
```

Audit is persisted with the package and is distinct from Provenance.

## 17. Serialization Rules

Serialization must preserve:

- Data types
- Units
- Versions
- Missing versus zero
- Array order
- OriginalRowIndex
- Event indices
- Audit information

Stored precision is independent of display precision. A formatted Excel value must never replace the full stored numeric value.

Missing/NULL is distinct from zero. Invalid values are represented with status information rather than silently converted to zero.

## 18. Array Integrity

Every analytical array records or can resolve:

```text
DatasetID
DatasetVersion
Length
IndexStart
IndexEnd
```

Force, Stress, Strain and other paired arrays must satisfy the approved dataset pairing and boundary rules.

## 19. Persistence

The logical persistence boundary is:

```text
Test
Source
Dataset
Events
Results
Corrections
Validation
Audit
```

Persistence is transactional/atomic:

```text
Begin Save
  ↓
Validate Package
  ↓
Persist
  ↓
Integrity Check
  ↓
Commit
```

An incomplete save must not be presented as a Finalized package.

## 20. Version Chain

Recalculation or material changes do not destroy the previous package:

```text
Package V1
   ↓
Package V2
   ↓
Package V3
```

Older finalized versions remain available and may become `SUPERSEDED` when a newer version is finalized.

## 21. Recalculation

Recalculation creates a new package/result version and records:

```text
PreviousVersion
NewVersion
Trigger
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

## 22. Package State

Supported lifecycle states:

```text
IMPORTED
NORMALIZED
CALCULATED
VALIDATED
FINALIZED
SUPERSEDED
FAILED
INCOMPLETE
```

Typical path:

```text
IMPORTED
  ↓
NORMALIZED
  ↓
CALCULATED
  ↓
VALIDATED
  ↓
FINALIZED
```

## 23. Integrity

The package may maintain:

```text
SourceHash
DatasetHash
ConfigurationHash
ResultHash
PackageHash
```

A failed integrity check marks the package as corrupted/incomplete and prevents use as a trusted Finalized package until resolved.

## 24. Package Manifest

A compact manifest should identify:

```text
PackageID
TestID
SchemaVersion
ApplicationVersion
MethodVersion
ConfigurationVersion
DatasetVersion
ResultVersion
QualityStatus
PackageHash
```

## 25. SQLite and Excel Persistence Boundary

If SQLite is used, it is a persistence adapter rather than the definition of the Domain Model:

```text
Domain Model
      ↓
Persistence Adapter
      ↓
SQLite
```

Excel Worksheets/Ribbon UI are presentation and interaction surfaces, not the definition of the domain model.

## 26. Export / Import

The package model must support future serialization/export without changing calculation logic:

```text
Package
 ↓
Export
 ├── JSON
 ├── SQLite
 └── Structured Excel
```

Imported packages must check `SchemaVersion` and apply versioned migration where required. Migration must not modify the original Raw Source.

## 27. MVP Boundary

MVP requires persistence of:

```text
PackageIdentity
Source
TestMetadata
Configuration
RawDataset
NormalizedDataset
Events
Results
Validation
QualityStatus
Provenance
Audit
```

The following remain outside the current MVP scope:

- Cloud synchronization
- Distributed storage
- Multi-user concurrent editing
- Digital-signature infrastructure
- External LIMS integration
- Machine real-time connection
- PLC/device control

## 28. Freeze Decisions

| ID | Decision |
|---|---|
| D-514 | Test Result Package is an independent Domain Package. |
| D-515 | PackageID, TestID and PackageVersion are distinct. |
| D-516 | SchemaVersion is independent of ApplicationVersion. |
| D-517 | Source File is immutable. |
| D-518 | RawDataset is immutable after successful import. |
| D-519 | Raw, Normalized and Derived Datasets are separate. |
| D-520 | OriginalRowIndex is preserved through transformations. |
| D-521 | Effective Configuration is stored as a test-time snapshot. |
| D-522 | Effective Material Library values are stored as a traceable snapshot. |
| D-523 | Events are independent Package records. |
| D-524 | Results have ResultID and ResultVersion. |
| D-525 | Graph display settings are separate from calculation data. |
| D-526 | Corrections never overwrite RawDataset. |
| D-527 | Missing and zero are distinct serialized states. |
| D-528 | Stored precision is independent from display precision. |
| D-529 | Dataset Array Integrity is validated. |
| D-530 | Final Save is atomic/transactional. |
| D-531 | Previous snapshots are retained after recalculation. |
| D-532 | Recalculation creates a new Package Version. |
| D-533 | Package has a defined State Lifecycle. |
| D-534 | Failed Packages cannot be Finalized. |
| D-535 | Superseded Versions are retained. |
| D-536 | Package Integrity is verifiable. |
| D-537 | SQLite is a Persistence Adapter, not the Domain Model. |
| D-538 | Excel Worksheets do not define the Domain Model. |
| D-539 | Serialization is independent of Excel layout. |
| D-540 | Schema Migration is versioned. |
| D-541 | Audit is persisted. |
| D-542 | Result-affecting information cannot remain Session-Only. |
| D-543 | Package Manifest identifies Version and Integrity. |
| D-544 | MVP covers output-file analysis only. |
| D-545 | PLC, Machine Control, Real-Time Integration and LIMS are outside TB-025 scope. |

**Status: Approved / Frozen — TB-025.**
