# TB-012 — ISO 6892-1 Stress/Strain Dataset Normalization, Units & Cross-Sectional Area Calculation Specification

**Document:** TB-012  
**Project:** MTDMS — Material Test Data Management System  
**Version:** 1.0  
**Status:** Approved / Frozen  
**Parent:** TB-005, TB-007, TB-008, TB-008.1, TB-009, TB-010, TB-011  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in  
**Calculation model:** Array-Based

## 1. Purpose

TB-012 defines the normalization layer that converts raw TXT output into an engineering Dataset for tensile-test calculations. Raw file values are never overwritten.

## 2. Raw Dataset

The approved raw columns are:

```text
No
Time
Displacement
Deformationt
Force
```

The raw arrays are preserved as:

```text
No()
Time()
Displacement()
Deformationt()
ForceRaw()
```

## 3. Force Unit

The file Force unit is **kgf**. Raw force remains in kgf. The normalized calculation force is N:

```text
ForceN(i) = ForceRaw(i) × 9.80665
```

Raw and normalized force are independent arrays.

## 4. Engineering Stress

For initial cross-sectional area `A0`:

```text
EngineeringStress(i) = ForceN(i) / A0
```

When Force is N and Area is mm², stress is N/mm² = MPa.

## 5. Initial Area

`A0` is an independent geometry parameter with an explicit source:

```text
MEASURED
CALCULATED
OPERATOR_ENTERED
METADATA
METHOD_DEFAULT
```

The calculation method is specimen/Method-specific.

## 6. Geometry Methods

Round specimen:

```text
A0 = π d0² / 4
```

Flat rectangular specimen:

```text
A0 = a0 × b0
```

Pipe/tube:

```text
A0 = π/4 × (Do² - Di²)
```

Pipe validation requires `Do > Di > 0`.

## 7. Metadata

The currently selected metadata fields are:

```text
Line 10 → d/a
Line 11 → b
Line 13 → L0
```

For TB-012, `L0` is available as a geometry input subject to validation. `d/a` and `b` remain metadata unless a selected Method explicitly defines their interpretation.

## 8. Crosshead Strain

When Crosshead is the active source:

```text
ΔL(i) = Displacement(i)
EngineeringStrain(i) = ΔL(i) / L0
```

## 9. Extensometer Strain

When Extensometer is the active source:

```text
ΔLe(i) = Deformationt(i)
EngineeringStrain(i) = Deformationt(i) / Le
```

where `Le` is the applicable extensometer gauge length defined by the Method/measurement configuration.

## 10. Source Segmentation

The final engineering strain array is generated from the approved source map. The normal project sequence is:

```text
CROSSHEAD → EXTENSOMETER → CROSSHEAD
```

Attach and Release are independent Events.

## 11. No Overwrite

Raw `Displacement()` and `Deformationt()` are never replaced by corrected or normalized values. Derived arrays are created separately.

## 12. Strain Representation

Engineering strain is stored internally as a dimensionless ratio:

```text
0.002 = 0.2 %
```

A separate display array may be used:

```text
StrainPercent(i) = EngineeringStrain(i) × 100
```

## 13. Internal Units

The preferred calculation units are:

```text
Force   → N
Length  → mm
Area    → mm²
Stress  → MPa
Strain  → ratio
```

Raw input units and normalized units remain traceable.

## 14. Dataset Index

Every record has an internal `DatasetIndex`. The file's `No` column is retained as raw source information and is not assumed to be the calculation index.

## 15. Invalid Rows

Invalid rows are not physically deleted from the raw dataset. Instead the system maintains masks such as:

```text
ValidRow(i)
CalculationEligible(i)
```

## 16. Zero and Duplicate Values

Zero Force, zero Displacement, duplicate timestamps, and initial zero rows are not automatically removed. They remain part of the raw dataset and are interpreted by the appropriate analysis method.

If Extensometer is not active, a zero `Deformationt` value is not by itself evidence of zero specimen strain. The source map determines whether the field is calculation-eligible.

## 17. Stress/Strain Pairing

Stress and strain must correspond to the same `DatasetIndex`. No silent index shifting is permitted.

## 18. Time Validation

Time should be non-decreasing. A decrease in time produces a validation warning or method-defined invalid state. Raw time remains unchanged.

## 19. Unit Conversion Layer

Conversion factors are centralized. They must not be duplicated across individual calculation procedures.

The kgf-to-N factor used by the normalization layer is:

```text
9.80665 N/kgf
```

## 20. Precision

Raw numeric precision is retained. Rounding is applied only for display, reporting, or explicitly configured export.

## 21. Normalized Dataset

```text
NormalizedDataset
├── DatasetIndex()
├── No()
├── Time()
├── Displacement()
├── Deformationt()
├── ForceRaw()
├── ForceN()
├── EngineeringStress()
├── EngineeringStrain()
├── StrainPercent()
├── StrainSource()
├── ValidRow()
└── CalculationEligible()
```

## 22. Pipeline

```text
Raw TXT
  ↓
Parse
  ↓
Raw Arrays
  ↓
Metadata
  ↓
Validation
  ↓
Unit Normalization
  ↓
Geometry / A0
  ↓
Force Normalization
  ↓
Stress Calculation
  ↓
Strain Source Engine
  ↓
Engineering Strain
  ↓
Normalized Dataset
```

## 23. Downstream Dependencies

```text
TB-012
   ├── TB-008 → Rp0.2
   ├── TB-009 → Rm / Fracture
   ├── TB-010 → Elongation / Gauge-Length Correction
   └── TB-011 → Elastic Region / E / Graph Correction
```

TB-012 is numerical normalization; TB-005 remains the source-decision layer.

## 24. Validation Summary

Each normalized Dataset exposes:

```text
RowCount
ValidRowCount
InvalidRowCount
ForceUnitValid
GeometryValid
L0Valid
A0Valid
TimeValid
StrainSourceValid
DatasetStatus
```

Dataset status:

```text
VALID
VALID_WITH_WARNINGS
INVALID
NOT_CALCULABLE
```

## 25. Data Lineage

Every calculated result must remain traceable:

```text
Result
 ↓
Normalized Array
 ↓
Raw Array
 ↓
TXT Row
```

For example:

```text
Rm
 ↓
EngineeringStress(i)
 ↓
ForceN(i)
 ↓
ForceRaw(i)
 ↓
TXT Row
```

## 26. Graph Correction Ordering

Graph correction occurs after normalization and analysis:

```text
Raw
 ↓
Normalize
 ↓
Calculate
 ↓
Analyze
 ↓
Correct Graph
```

It must not operate directly on unnormalized raw force/strain values.

## 27. Uncertainty Scope

Uncertainty propagation for force, dimensions, area and stress is outside the scope of TB-012 and requires a dedicated uncertainty specification.

## 28. Freeze Decisions

| ID | Decision |
|---|---|
| D-189 | Force raw file values are retained in kgf. |
| D-190 | Calculation force is normalized to N. |
| D-191 | Raw and normalized force are independent arrays. |
| D-192 | Engineering stress is calculated from ForceN and A0. |
| D-193 | With N/mm², stress is represented as MPa. |
| D-194 | Engineering strain is stored as a dimensionless ratio. |
| D-195 | StrainPercent is a derived display representation. |
| D-196 | L0 comes from Metadata line 13 subject to validation. |
| D-197 | Metadata lines 10 and 11 remain metadata until a Method defines their interpretation. |
| D-198 | A0 is an independent parameter with an explicit source. |
| D-199 | A0 calculation depends on specimen geometry and Method. |
| D-200 | Raw Dataset is never overwritten. |
| D-201 | Invalid rows are not deleted from Raw Dataset. |
| D-202 | Validity masks control row eligibility. |
| D-203 | Stress and strain must use the same DatasetIndex. |
| D-204 | Zero Force and zero Displacement rows are not automatically removed. |
| D-205 | Zero Deformationt alone does not prove zero strain. |
| D-206 | Unit conversion is centralized. |
| D-207 | Internal calculations are not prematurely rounded. |
| D-208 | Graph correction occurs after normalization. |
| D-209 | Uncertainty calculation is outside TB-012 scope. |
| D-210 | Result-to-raw-row Data Lineage is mandatory. |

## 29. Deferred Rules

The following remain Method-specific until verified against the authorized ISO 6892-1 implementation and project data:

- exact A0 determination rules for each specimen type;
- interpretation of `d/a` and `b`;
- exact Crosshead strain treatment;
- exact Crosshead/Extensometer boundary handling;
- exact handling of initial zero rows in each analysis method;
- exact export-unit requirements.

## 30. Status

**Approved / Frozen — TB-012.**
