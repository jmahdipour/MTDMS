# TB-004 — Engineering Calculation Pipeline

**Document:** TB-004  
**Project:** MTDMS — Material Test Data Management System  
**Version:** 1.0  
**Status:** Approved / Frozen  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in  
**Calculation model:** Array-based

---

## 1. Purpose

TB-004 defines the engineering calculation pipeline between the imported `EngineeringDataset` and engineering results.

The pipeline must keep raw source data immutable and must keep calculated data separate from graph-corrected visualization data.

```text
Raw Arrays
 ↓
Derived Arrays
 ↓
Event Detection / Selection
 ↓
Engineering Results
 ↓
Graph Correction
```

No calculation is performed directly from Worksheet cells.

---

## 2. Calculation Inputs

From TB-002/TB-003:

```text
Metadata
├── DiameterOrArea   ← TXT line 10
├── Width            ← TXT line 11
└── InitialLength    ← TXT line 13

RawData
├── No()
├── Time()
├── Displacement()
├── Deformationt()
└── Force()          ← kgf
```

Later analysis inputs:

```text
Selection
├── YieldPoint
├── ExtensometerReleasePoint
├── FracturePoint
├── SecondaryLength
└── StrainSegments()
```

---

## 3. Raw Force

The imported force remains:

```text
ForceRaw(i) = kgf
```

It is never overwritten by the SI conversion.

---

## 4. Force Conversion

For SI-based engineering calculations:

```text
ForceN(i) = ForceRaw(i) × 9.80665
```

The result is stored in a separate array:

```text
ForceRaw()
ForceN()
```

The raw kgf value remains the authoritative imported value.

---

## 5. Cross-Sectional Area

The calculation of `A0` is dependent on the approved specimen geometry/configuration.

The parser must not infer the meaning of `d/a`.

For example, where a circular specimen diameter `d` is explicitly selected:

```text
A0 = πd² / 4
```

Other specimen geometries require their own approved geometry contract.

TB-004 does not freeze a geometry formula that has not yet been approved for the corresponding specimen type.

---

## 6. Engineering Stress

After `A0` has been resolved in mm²:

```text
EngineeringStress(i) = ForceN(i) / A0
```

When force is N and area is mm², the resulting unit is MPa because:

```text
1 MPa = 1 N/mm²
```

The output is a separate array:

```text
EngineeringStress()
```

---

## 7. Engineering Strain — Segmented Source Model

There is no single global strain source.

The approved architecture supports source segments such as:

```text
Segment 1 → EXTENSOMETER
Segment 2 → CROSSHEAD
```

The final `EngineeringStrain()` array is assembled from the applicable source segment while retaining the original point indexes.

---

## 8. Extensometer Strain

Within an approved valid extensometer segment:

```text
StrainExt(i) = Deformationt(i) / L0
```

and percentage strain is:

```text
StrainExtPercent(i) = 100 × Deformationt(i) / L0
```

The raw `Deformationt()` array is never modified.

---

## 9. Crosshead Strain

Within an approved crosshead segment:

```text
StrainCH(i) = DisplacementRelativeToApprovedOrigin(i) / L0
```

The exact crosshead origin/zero reference remains an explicit analysis configuration item rather than an implicit assumption.

The raw `Displacement()` array is never modified.

---

## 10. Strain Source Array

Each point may have an associated source:

```text
StrainSource(i)
```

Example:

```text
1 ... 850       → EXTENSOMETER
851 ... 4200    → CROSSHEAD
```

The boundary is determined by the independently defined `ExtensometerReleasePoint`, not by assuming that release equals yield.

---

## 11. Independent Engineering Events

The following events remain independent:

```text
YieldPoint
≠
ExtensometerReleasePoint
≠
FracturePoint
```

Any of the three may occur at different indexes.

The calculation engine must never silently equate them.

---

## 12. Young's Modulus

Young's modulus is calculated from the selected elastic region.

Conceptual flow:

```text
EngineeringStress()
        +
EngineeringStrain()
        ↓
Regression Window
        ↓
Linear Regression
        ↓
Slope / Intercept / R²
        ↓
Young's Modulus
```

The modulus result must retain:

```text
E
Slope
Intercept
R²
StartIndex
EndIndex
StrainSource
```

and the applicable calculation method/version.

---

## 13. Material Library Reference

Material Library may provide:

```text
E_reference
```

but:

```text
E_reference ≠ E_test
```

The measured test value is calculated from the actual Dataset.

Material Library is used only as reference, guidance, or plausibility information unless a separately approved method says otherwise.

---

## 14. Yield Calculation

Yield detection is independent from extensometer release.

Possible methods:

```text
AUTO
MANUAL
LIBRARY_ASSISTED
```

Inputs may include:

```text
EngineeringStress()
EngineeringStrain()
YoungModulus
MaterialReference
```

Outputs include at least:

```text
YieldPoint
YieldStress
YieldStrain
DetectionMethod
```

Material Library yield values may define a candidate/search region or warning threshold, but they do not automatically replace the measured result.

---

## 15. UTS

Ultimate tensile strength is the maximum engineering stress within the approved test region:

```text
UTS = Max(EngineeringStress())
```

The corresponding point index must also be retained:

```text
UTSIndex
```

Only the numeric maximum is insufficient for traceability.

---

## 16. Fracture Point

Fracture is an independent event:

```text
FracturePoint
```

It retains at least:

```text
Index
Time
Force
Stress
Strain
DetectionMethod
OperatorConfirmed
```

Fracture detection and confirmation are separate from the source-switch event.

---

## 17. True Stress / True Strain

True stress and true strain are separate derived arrays:

```text
TrueStress()
TrueStrain()
```

They are calculated only after the approved engineering method and valid range have been established.

They must not overwrite engineering stress/strain arrays or raw data.

---

## 18. Post-Fracture Elongation

After fracture, the operator may provide the measured secondary gauge length:

```text
L0 = Original Gauge Length
L2 = Post-Fracture Measured Gauge Length
```

Post-fracture elongation is calculated as:

```text
A% = ((L2 - L0) / L0) × 100
```

This is an independent result and is not assumed to equal instantaneous strain at the fracture point.

Provenance must include `L0`, `L2`, measurement method, operator, and timestamp.

---

## 19. Graph Correction

Graph Correction is downstream of engineering calculation:

```text
Raw
 ↓
Calculated
 ↓
Events
 ↓
Material Reference
 ↓
Secondary Length
 ↓
Graph Correction
 ↓
Corrected Visualization
```

Graph Correction creates new derived visualization arrays such as:

```text
CorrectedStrain()
```

and/or corrected horizontal-axis values.

It must never overwrite RawData.

---

## 20. Secondary Length and Horizontal Axis Scaling

The operator-measured `L2` may be used during Graph Correction to scale the horizontal axis where required by the approved engineering method.

`L0` and `L2` remain separate values.

The correction must retain:

```text
ScaleFactor
CorrectionMethod
L0
L2
CorrectionTimestamp
Operator
```

The corrected graph is a derived visualization, not a replacement for the raw or calculated Dataset.

---

## 21. Three Data Layers

The calculation architecture has three distinct layers:

```text
┌─────────────────────────┐
│ RAW DATA                │
│ ForceRaw                │
│ DisplacementRaw         │
│ DeformationtRaw         │
└────────────┬────────────┘
             ↓
┌─────────────────────────┐
│ CALCULATED DATA         │
│ ForceN                  │
│ Stress                  │
│ Strain                  │
│ True Stress/Strain      │
└────────────┬────────────┘
             ↓
┌─────────────────────────┐
│ CORRECTED VISUALIZATION │
│ CorrectedStrain         │
│ Corrected Axis          │
└─────────────────────────┘
```

This separation is mandatory for traceability.

---

## 22. Calculation Pipeline

```text
ForceRaw (kgf)
       │
       ▼
ForceN
       │
       ▼
Cross-Section Area
       │
       ▼
Engineering Stress
       │
       ├───────────────────┐
       │                   │
       ▼                   ▼
Extensometer          Crosshead
       │                   │
       └─────────┬─────────┘
                 ▼
        Segmented Strain
                 │
       ┌─────────┼─────────┐
       ▼         ▼         ▼
       E       Yield      UTS
       │         │         │
       └─────────┼─────────┘
                 ▼
             Fracture
                 │
                 ▼
       True Stress / Strain
                 │
                 ▼
        Secondary Length
                 │
                 ▼
         Graph Correction
                 │
                 ▼
       Corrected Visualization
```

---

## 23. Array-Based Rule

Every point-wise calculation must operate on aligned arrays using the same master point index.

Examples:

```text
ForceRaw(i)
ForceN(i)
EngineeringStress(i)
EngineeringStrain(i)
TrueStress(i)
TrueStrain(i)
StrainSource(i)
PointStatus(i)
```

A calculation may use a defined index range, but it must never independently reorder the point arrays.

---

## 24. Result Traceability

Every important result must retain enough information to reproduce and audit it.

Conceptual structure:

```text
Result
├── Value
├── Unit
├── Method
├── InputRange
├── Source
├── RegressionInformation
├── CalculationVersion
└── Provenance
```

For modulus, this includes the regression range, slope, R², strain source, and calculation method.

---

## 25. Explicitly Deferred Geometry Decisions

The exact Area formula is not frozen globally by TB-004.

The reason is that `d/a` on line 10 has not been approved as a universal interpretation for every specimen type.

The final geometry method must be selected from the approved specimen/test configuration.

Similarly, the exact Crosshead origin/zero rule remains an explicit analysis configuration item.

No undocumented assumption may be introduced merely to complete a calculation.

---

## 26. Approved Design Decisions

| ID | Decision |
|---|---|
| D-31 | All engineering calculations are array-based. |
| D-32 | Raw Force remains kgf in the raw Dataset. |
| D-33 | Newton conversion creates a separate `ForceN()` array. |
| D-34 | Engineering stress is stored separately from raw force. |
| D-35 | Strain is assembled from independently defined source segments. |
| D-36 | Extensometer and Crosshead strain are separate derived sources. |
| D-37 | YieldPoint, ExtensometerReleasePoint, and FracturePoint remain independent events. |
| D-38 | Young's modulus is calculated from the selected elastic regression range. |
| D-39 | Material Library provides reference/guidance and does not impose measured results. |
| D-40 | UTS retains both value and source point index. |
| D-41 | True stress/strain are separate derived arrays. |
| D-42 | Post-fracture elongation uses operator-measured L2 together with original L0. |
| D-43 | L2 never replaces L0. |
| D-44 | Graph Correction creates separate corrected visualization data. |
| D-45 | Raw and calculated data are never overwritten by Graph Correction. |
| D-46 | Exact geometry formulas remain configuration-dependent until approved. |
| D-47 | Exact Crosshead origin/zero handling remains an explicit configuration item until approved. |

---

## 27. Next Blueprint

**TB-005 — Strain Source Segmentation & Event Engine**

The next document will define how `YieldPoint`, `ExtensometerReleasePoint`, and `FracturePoint` are represented on the master arrays, how source segments are bounded, how operator confirmation works, and how Extensometer/Crosshead strain is assembled without changing raw data.

No application code is defined by this document.
