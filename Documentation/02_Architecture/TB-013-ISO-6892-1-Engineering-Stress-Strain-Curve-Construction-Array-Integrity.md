# TB-013 — ISO 6892-1 Engineering Stress–Strain Curve Construction & Array Integrity Specification

**Document:** TB-013  
**Project:** MTDMS — Material Test Data Management System  
**Version:** 1.0  
**Status:** Approved / Frozen  
**Parent:** TB-005 through TB-012  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in  
**Calculation model:** Array-Based

## 1. Purpose

TB-013 defines construction of the engineering Stress–Strain curve from the normalized Dataset defined in TB-012. The graph is a view of calculation arrays; numerical results are never extracted from graph pixels.

## 2. Array-Based Principle

The calculation layer uses arrays such as:

```text
ForceN()
EngineeringStress()
EngineeringStrain()
StrainSource()
DatasetIndex()
ValidRow()
CalculationEligible()
```

Raw data is never overwritten.

## 3. Engineering Stress

```text
EngineeringStress(i) = ForceN(i) / A0
```

With Force in N and Area in mm², the result is MPa.

## 4. Engineering Strain

`EngineeringStrain(i)` is supplied by the approved strain-source map from TB-005 and TB-012. The project source sequence is:

```text
CROSSHEAD → EXTENSOMETER → CROSSHEAD
```

Extensometer Attach and Release are independent Events.

## 5. Matched Curve Point

Each curve point is the same Dataset Index:

```text
Point(i) = (EngineeringStrain(i), EngineeringStress(i))
```

No silent index shifting, sorting, or mismatched pairing is permitted.

## 6. Dataset Order

Curve points preserve Dataset/Time order. Stress and strain arrays are never sorted by magnitude.

## 7. Validity

A point is eligible for the engineering curve only when its validity and calculation masks permit it and both stress and strain are valid. Invalid rows remain in the Raw Dataset.

## 8. Initial Zero Rows

Initial zero-force and zero-displacement rows are not automatically deleted. They may represent origin, preload, seating, or initial-state information and are interpreted by the applicable Method.

## 9. Extensometer Boundary

The curve may contain separate strain-source segments. Source transitions must remain traceable and must not be silently merged into one source.

Example:

```text
1–800       CROSSHEAD
801–1500    EXTENSOMETER
1501–3000   CROSSHEAD
```

## 10. Discontinuity at Source Change

If the source transition produces a scale or value discontinuity, the graph engine must not create an artificial connecting correction. Any normalization or correction must be explicitly defined by the applicable Method.

## 11. Curve Rendering

The engineering curve is:

```text
X = EngineeringStrain
Y = EngineeringStress
```

Recommended display units are strain (%) and stress (MPa), while calculation arrays retain ratio strain and MPa.

## 12. Deformationt

`Deformationt` contributes to engineering strain only when `StrainSource = EXTENSOMETER`. When Crosshead is active, Crosshead displacement and L0 govern the strain calculation according to the approved method.

## 13. Yield, Rp0.2, Rm and Fracture

Yield, Rp0.2, Rm and Fracture are derived results referencing Dataset Indices. Their graph markers are overlays and do not modify the underlying arrays.

## 14. Fracture Boundary

Raw data after fracture remains available. The curve display/analysis end index is controlled by TB-009/TB-010 and the applicable Method; post-fracture data is not physically deleted.

## 15. Calculation Dataset vs Graph View

These are separate concepts:

```text
CalculationDataset
GraphViewDataset
```

Graph View may restrict the displayed range without changing calculation data.

## 16. Graph Correction

Horizontal-axis correction creates a derived array:

```text
CorrectedStrain()
```

and never overwrites `EngineeringStrain()`.

Where the configured method specifies the multiplicative correction model:

```text
CorrectedStrain(i) = EngineeringStrain(i) × CorrectionFactor
```

Stress remains unchanged.

## 17. Curve Integrity After Correction

For the same view range:

```text
CorrectedStrain(i)
↔ EngineeringStress(i)
↔ EngineeringStrain(i)
↔ DatasetIndex(i)
```

The number of curve points is not changed by axis correction.

## 18. Interpolation and Smoothing

Interpolation, spline fitting, smoothing, or resampling may be used only as explicitly configured display operations. They must not silently replace the calculation Dataset used for numerical results.

## 19. Manual Graph Selection

An operator may click a point on the graph. The selected screen coordinate is mapped to the nearest/appropriate Dataset Index, and calculations operate on that Dataset Index—not on pixel coordinates.

## 20. Manual Yield Selection

Manual yield selection is recorded as an independent event containing at least:

```text
DatasetIndex
Operator
Timestamp
Reason
Comment
```

Automatic candidates remain traceable after a manual override.

## 21. Analysis Overlays

Analysis overlays may include:

```text
Elastic Line
Rp0.2 Offset
Yield Marker
Rm Marker
Fracture Marker
Correction Guide
```

They are View/Analysis objects and do not alter the calculation arrays.

## 22. Reporting

Analysis overlays are not included in the final report by default. Only approved results and configured report elements are exported.

## 23. Curve Metadata

Each curve retains:

```text
CurveMetadata
├── DatasetID
├── MethodID
├── Standard
├── StressUnit
├── StrainUnit
├── StrainSourceModel
├── CorrectionState
└── CalculationVersion
```

## 24. Integrity Checks

Before analysis:

```text
Length(Stress) = Length(Strain)
Length(Stress) = Length(DatasetIndex)
```

must hold for the selected curve Dataset.

Failure results in:

```text
Curve.Status = INVALID
```

No dependent numerical result is generated from an invalid curve structure.

## 25. Non-Numeric Values

Empty, Null, Error, NaN, and non-numeric values are not accepted into the valid calculation arrays. Their Raw Dataset records remain preserved and traceable.

## 26. Negative Values

Negative Stress or Strain values are not automatically deleted. Their treatment is Method-specific because they may represent zero correction, unloading, machine return, or other valid/invalid states.

## 27. Unloading

The curve engine does not assume complete monotonicity. Unloading regions remain in the Dataset and are interpreted by the applicable analysis method.

## 28. Numerical Results

Numerical results including:

```text
Yield
Rp0.2
Rm
Fracture
Elongation
Young’s Modulus
```

must originate from calculation arrays and method logic, never graph pixels.

## 29. Provenance

```text
CurveProvenance
├── DatasetID
├── FirstIndex
├── LastIndex
├── PointCount
├── StrainSource
├── StressFormulaVersion
├── StrainFormulaVersion
├── AreaSource
├── L0Source
└── CalculationVersion
```

## 30. Architecture

```text
NormalizedDataset
        ↓
CurveDataset
        ↓
Analysis Engine
        ↓
Results / Graph View
```

The Curve Dataset does not modify the Raw Dataset.

## 31. CurveDataset

```text
CurveDataset
├── DatasetIndex()
├── Stress()
├── Strain()
├── Source()
├── Valid()
├── Eligible()
└── ViewState
```

## 32. ViewState

```text
ViewState
├── StartIndex
├── EndIndex
├── CorrectionApplied
├── CorrectionFactor
├── ShowAnalysisOverlay
└── ShowPostFracture
```

## 33. Calculation Version

Every calculated curve/result retains a calculation version so results from different algorithm versions remain distinguishable.

## 34. Freeze Decisions

| ID | Decision |
|---|---|
| D-211 | Engineering Stress and Engineering Strain are generated as calculation arrays. |
| D-212 | Stress and strain use a common Dataset Index. |
| D-213 | Curve order follows Dataset/Time order. |
| D-214 | Stress and strain are never sorted. |
| D-215 | Raw Dataset is never overwritten. |
| D-216 | Zero rows are not automatically deleted. |
| D-217 | Extensometer Attach and Release define strain-source boundaries. |
| D-218 | Crosshead and Extensometer data are not silently merged without the Source Map. |
| D-219 | The graph is a view of calculation arrays. |
| D-220 | Numerical results are never extracted from pixels or screen coordinates. |
| D-221 | Graph correction creates a separate derived strain array. |
| D-222 | Graph correction does not modify Stress. |
| D-223 | Graph correction does not change calculation point count. |
| D-224 | Display interpolation/smoothing must not replace calculation arrays. |
| D-225 | Manual graph selection maps to DatasetIndex. |
| D-226 | Manual Yield Selection is recorded as an Event. |
| D-227 | Analysis overlays are excluded from the final report by default. |
| D-228 | Array-length mismatch makes the curve INVALID. |
| D-229 | Raw invalid records remain preserved. |
| D-230 | Curve results retain provenance and CalculationVersion. |

## 35. Status

**Approved / Frozen — TB-013.**
