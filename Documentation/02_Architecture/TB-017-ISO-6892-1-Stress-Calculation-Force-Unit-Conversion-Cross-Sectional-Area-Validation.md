# TB-017 — ISO 6892-1 Stress Calculation, Force Unit Conversion & Cross-Sectional Area Validation Specification

**Document:** TB-017  
**Project:** MTDMS — Material Test Data Management System  
**Version:** 1.0  
**Status:** Approved / Frozen  
**Parent:** TB-005 → TB-016  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in  
**Calculation model:** Array-Based

## 1. Purpose

TB-017 defines conversion of raw Force to calculation Force and construction of Engineering Stress, including force-unit, area-unit, specimen-geometry and cross-sectional-area validation.

## 2. Core Formula

```text
EngineeringStress = ForceN / A0_mm2
```

When Force is N and Area is mm², Stress is MPa because 1 N/mm² = 1 MPa.

## 3. Raw Data Preservation

Raw Force, Displacement, Deformationt and all original Dataset rows are never overwritten or deleted by unit conversion, area calculation or stress calculation.

## 4. Force Units

The Force unit must be explicitly established from the file definition, approved import mapping or Method configuration. The system must not guess a unit from the numeric magnitude.

Supported conversions may include N, kN, kgf, gf and lbf when explicitly configured.

```text
kN → N: F_N = F_kN × 1000
kgf → N: F_N = F_kgf × 9.80665
lbf → N: F_N = F_lbf × 4.4482216152605
```

Conversion factors and rules are versioned and traceable.

## 5. Area Units

The preferred internal area unit is mm². Supported input units may include mm², cm², m² and in² when explicitly mapped.

## 6. Initial Cross-Sectional Area

`A0` is the initial specimen cross-sectional area. For Engineering Stress it is constant across the Dataset unless an applicable Method explicitly defines another model.

## 7. Geometry Types

The Geometry Engine may support:

```text
ROUND
RECTANGULAR
TUBULAR
OTHER_METHOD_DEFINED
```

### Round

```text
A0 = π d² / 4
```

### Rectangular

```text
A0 = a × b
```

### Tubular

```text
A0 = π(D² - d²) / 4
```

Geometry interpretation must be established by an approved mapping; metadata values must not be assigned a meaning by guesswork.

## 8. Geometry Validation

Before stress calculation:

```text
Geometry
→ Unit Validation
→ Area Calculation
→ Area Validation
→ Stress Calculation
```

Dimensions must be numeric and greater than zero. Blank, text, nonnumeric, zero or negative dimensions are invalid.

## 9. Invalid Area

```text
A0 = 0  → INVALID_AREA
A0 < 0  → INVALID_AREA
A0 Missing → MISSING_AREA
```

Stress is not fabricated when Area is invalid or missing.

## 10. Stress Array

The calculation layer maintains separate arrays:

```text
ForceRaw()
ForceN()
ForceUnit()

Area0
AreaMM2
AreaUnit()

EngineeringStress()
StressUnit
```

Every calculated stress retains DatasetIndex traceability.

## 11. Zero Force

If `ForceN(i)=0` and Area is valid, `EngineeringStress(i)=0`. The row remains in the Dataset.

## 12. Negative Force

Negative Force is preserved. The system must not automatically apply `ABS(Force)`.

Negative Engineering Stress may therefore exist and remains subject to Method validity rules.

## 13. Missing / Invalid Force

If a Force value is missing or invalid:

```text
ForceN(i) = NA
EngineeringStress(i) = NA
```

The Dataset row is retained and its DatasetIndex remains available.

`Missing ≠ 0`.

## 14. Precision

Calculation precision is independent of display precision. Area must not be rounded for display before Stress calculation. Rounding is applied only at presentation/export stages unless a specific Method rule requires otherwise.

## 15. Manual Area Correction

An operator may create a `ManualAreaCorrectionEvent` containing at least:

```text
OldArea
NewArea
Operator
Timestamp
Reason
```

Changing A0 rebuilds the derived Stress array and dependent results without changing Raw Dataset values.

## 16. Engineering vs True Stress

TB-017 defines Engineering Stress as:

```text
EngineeringStress = Force / A0
```

True Stress is a separate derived Method and must never silently replace Engineering Stress.

## 17. Validity Boundary

A stress value can be numerically calculable while being outside the valid analysis region. Therefore:

```text
Calculated ≠ ValidForMethod
```

The Valid Test Region and terminal boundaries are supplied by the relevant Method/Event specifications, including TB-009.

## 18. Rm and Rp0.2

TB-008 and TB-009 consume the validated Engineering Stress and Engineering Strain arrays. Changes to valid Area trigger recalculation of dependent results.

## 19. Outliers

TB-017 does not delete or automatically correct outliers. Quality/analysis layers may flag them while preserving the original Dataset.

## 20. Traceability

Stress must be reconstructable through:

```text
EngineeringStress
→ ForceN
→ ForceRaw
→ Original TXT Dataset Row
```

and:

```text
EngineeringStress
→ A0
→ Geometry Metadata / Operator Correction
```

## 21. Pipeline

```text
Raw TXT
   ↓
Force Validation
   ↓
Force Unit Conversion
   ↓
Geometry Validation
   ↓
Area Calculation
   ↓
Area Validation
   ↓
Engineering Stress
   ↓
Valid Test Region
   ↓
TB-008 / TB-009 / TB-011
```

## 22. Freeze Decisions

| ID | Decision |
|---|---|
| D-291 | Engineering Stress is calculated from F/A0. |
| D-292 | A0 is the initial specimen cross-sectional area. |
| D-293 | A0 is constant for Engineering Stress unless an applicable Method explicitly defines another model. |
| D-294 | Force Unit must be explicit and traceable. |
| D-295 | The system must not guess Force Unit. |
| D-296 | Internal Force for Stress calculation is N. |
| D-297 | Preferred internal Area unit is mm². |
| D-298 | N/mm² is MPa. |
| D-299 | Raw Force is never overwritten. |
| D-300 | Negative Force is not automatically converted with ABS. |
| D-301 | Zero or negative Area is invalid. |
| D-302 | Missing Area prevents Stress calculation. |
| D-303 | Geometry is validated before Stress calculation. |
| D-304 | Display rounding must not alter calculation precision. |
| D-305 | Unit conversion factors and formulas are traceable and versioned. |
| D-306 | Engineering Stress and True Stress are independent. |
| D-307 | Area correction rebuilds Derived Stress and dependent results. |
| D-308 | Area correction does not modify Raw Dataset. |
| D-309 | Missing is not equivalent to Zero. |
| D-310 | Invalid Rows are retained and DatasetIndex is preserved. |
| D-311 | TB-017 does not delete Outliers. |
| D-312 | Valid Stress Region is controlled by the applicable Method/Boundary Engine. |
| D-313 | Rp0.2 and Rm use the validated Engineering Stress array. |
| D-314 | Stress is traceable to Raw Force and Geometry. |
| D-315 | Calculations are Array-Based. |

## 23. Status

**Approved / Frozen — TB-017.**
