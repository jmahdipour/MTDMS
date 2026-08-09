# TB-010 — ISO 6892-1 Elongation After Fracture, Gauge-Length Measurement & Horizontal Axis Correction Specification

**Document:** TB-010  
**Project:** MTDMS — Material Test Data Management System  
**Version:** 1.0  
**Status:** Approved / Frozen  
**Parent:** TB-007, TB-008, TB-008.1, TB-009  
**Standard:** ISO 6892-1:2019  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in  
**Calculation model:** Array-Based

## 1. Scope

TB-010 defines three separate but related concepts:

1. Elongation After Fracture;
2. final gauge-length measurement;
3. horizontal-axis graph correction.

Graph correction is an analysis/visualization layer and must not silently modify raw TXT data or mechanical results.

## 2. Geometry Parameters

The following remain independent:

```text
L0
Lu
Le
SecondaryLength
A0
```

- `L0`: original gauge length;
- `Lu`: measured final gauge length after fracture;
- `Le`: extensometer gauge length;
- `SecondaryLength`: operator-measured length used by the graph-correction workflow;
- `A0`: original cross-sectional area.

## 3. Metadata Inputs

Per the current project decision, only these metadata fields are consumed at this stage:

```text
Line 10 → d/a
Line 11 → b
Line 13 → L0
```

Other metadata is retained but is outside the current calculation scope.

## 4. Force Units

The raw Force column is in kgf:

```text
ForceRaw(i) = kgf
```

The calculation array is:

```text
ForceN(i) = ForceRaw(i) × 9.80665
```

Raw Force is never overwritten.

## 5. Deformationt

`Deformationt` contains extensometer deformation when the extensometer is active.

Its validity is controlled by the strain-source segmentation defined in TB-008.1.

Raw `Deformationt()` remains retained after extensometer release.

## 6. Elongation After Fracture

Where the applicable method requires final gauge-length measurement:

```text
A = ((Lu - L0) / L0) × 100
```

`Lu` is a post-test physical measurement and is not automatically the last TXT displacement or strain value.

## 7. Lu Measurement

The operator may enter `Lu` with:

```text
Value
Unit
Operator
Timestamp
MeasurementMethod
Comment
```

`Lu` never overwrites `L0`.

## 8. Lu Validation

A valid measured value must satisfy the configured method requirements. As a basic data-quality check:

```text
Lu > 0
L0 > 0
```

If a positive elongation is expected and `Lu < L0`, the result receives `WARNING` or `INVALID` according to the configured method rule; the system must not silently accept it as a normal result.

## 9. Missing Lu

If the applicable method requires `Lu` and it is not supplied:

```text
ElongationAfterFracture.Status = NOT_AVAILABLE
```

The engine must not substitute final calculated strain without an explicit method rule.

## 10. L0 / Lu / Le Separation

The following distinction is mandatory:

```text
L0 ≠ Lu
L0 ≠ Le
Lu ≠ Le
```

unless a specific approved method explicitly establishes an equivalence for a particular specimen/test configuration.

## 11. SecondaryLength

`SecondaryLength` is an operator-provided measurement used by the project's graph-correction workflow.

By default:

```text
SecondaryLength ≠ Lu
SecondaryLength ≠ L0
SecondaryLength ≠ Le
```

A method-specific configuration may explicitly map them, but no implicit mapping is permitted.

## 12. Horizontal Axis Correction

The correction operates on a calculated horizontal array, not on the raw TXT data:

```text
Raw Dataset
   ↓
Calculated Strain
   ↓
Graph Correction
   ↓
CorrectedStrain()
```

The raw arrays remain immutable.

## 13. Corrected Arrays

A separate calculated representation is maintained, for example:

```text
CorrectedDisplacement()
CorrectedStrain()
```

The exact array used depends on the configured graph-correction method.

## 14. Correction Factor

A scale factor may be represented conceptually as:

```text
ScaleFactor = ReferenceLength / MeasuredLength
```

The exact choice of `ReferenceLength` and `MeasuredLength` is method-configured and must not be hard-coded globally.

## 15. Y Axis

The current project requirement treats the stress/force-derived vertical axis as the trusted axis during horizontal graph correction.

Therefore the correction primarily affects:

```text
X axis
```

and must not silently modify:

```text
Force
Stress
A0
```

## 16. Young's Modulus Verification

Graph Analysis may use the approved Young's modulus from the Material Library as a reference for checking the corrected elastic region.

Material Library values do not silently replace measured modulus values in the calculation engine.

## 17. Calculation vs Visualization Correction

Two distinct pipelines exist:

### Calculation

```text
Dataset
 ↓
Method Engine
 ↓
Mechanical Results
```

### Visualization

```text
Calculated Dataset
 ↓
Graph Correction
 ↓
Corrected Graph Dataset
```

Graph correction does not automatically trigger a new mechanical-result calculation.

If corrected data is explicitly intended to affect a result, the approved Method Engine must be rerun on the corrected dataset and the new calculation version recorded.

## 18. Correction Preconditions

Graph correction requires a valid `SecondaryLength` when that parameter is part of the configured method.

If it is absent or invalid:

```text
GraphCorrection.Status = NOT_AVAILABLE
```

## 19. SecondaryLength Validation

Minimum data-quality rule:

```text
SecondaryLength > 0
```

Otherwise:

```text
GraphCorrection.Status = INVALID
```

## 20. Graph Correction Event

Every manual/confirmed correction is traceable as an Event:

```text
GraphCorrectionEvent
├── EventID
├── CorrectionType
├── ReferenceLength
├── MeasuredLength
├── ScaleFactor
├── Operator
├── Timestamp
├── Reason
├── Comment
├── PreviousState
└── NewState
```

## 21. Correction States

```text
NOT_CORRECTED
CALCULATED
MANUAL_CONFIRMED
MANUAL_REJECTED
INVALID
```

## 22. Changing SecondaryLength

If the operator changes `SecondaryLength`:

```text
Old SecondaryLength
        ↓
New SecondaryLength
        ↓
Recalculate ScaleFactor
        ↓
Recalculate CorrectedStrain()
```

Raw data remains unchanged.

## 23. Fracture Independence

`FractureIndex` is determined from the analysis dataset according to TB-009.

Graph correction changes only the representation:

```text
FractureIndex
      ↓
CorrectedStrain(FractureIndex)
```

It does not move the physical fracture sample in the raw dataset.

## 24. Elongation Independence

Elongation After Fracture remains based on the applicable final gauge-length method:

```text
L0 + Lu
```

and not merely:

```text
CorrectedStrain(FractureIndex)
```

Therefore:

```text
Graph Correction ≠ Elongation After Fracture
```

## 25. Corrected Dataset

The system may maintain:

```text
OriginalDataset
CorrectedDataset
```

A corrected dataset can contain:

```text
No
Time
CorrectedDisplacement
CorrectedStrain
Stress
Force
```

The Original Dataset is always retained.

## 26. Export

An export of corrected graph data follows:

```text
Raw TXT
 ↓
Original Dataset
 ↓
Graph Correction
 ↓
Corrected Dataset
 ↓
ISO-format Export
```

The exported corrected dataset must retain correction provenance.

## 27. Provenance

```text
GraphCorrectionProvenance
├── DatasetID
├── CorrectionVersion
├── CorrectionType
├── L0
├── SecondaryLength
├── ReferenceLength
├── ScaleFactor
├── Operator
├── Timestamp
└── Method
```

Elongation provenance includes:

```text
ElongationProvenance
├── DatasetID
├── L0
├── Lu
├── ElongationPercent
├── MeasurementMethod
├── Operator
├── Timestamp
└── CalculationVersion
```

## 28. Report Rules

The final report may contain:

```text
L0
Lu
Elongation After Fracture
```

Analysis-only guides such as scale guides, elastic guides, correction guides, and candidate markers are not automatically included in the final report.

## 29. Array-Based Requirement

All TB-010 calculations are array-based:

```text
ForceRaw()
ForceN()
Displacement()
Deformationt()
EngineeringStress()
EngineeringStrain()
CorrectedStrain()
```

No result may be derived from graph pixels.

## 30. Status Model

Elongation:

```text
VALID
WARNING
INVALID
NOT_AVAILABLE
MANUAL
```

Graph Correction:

```text
NOT_CORRECTED
CALCULATED
MANUAL_CONFIRMED
MANUAL_REJECTED
INVALID
NOT_AVAILABLE
```

## 31. Freeze Decisions

| ID | Decision |
|---|---|
| D-153 | `L0`, `Lu`, `Le`, and `SecondaryLength` are independent parameters. |
| D-154 | `Lu` is the measured final gauge length after fracture. |
| D-155 | Where applicable, elongation after fracture is calculated as `((Lu-L0)/L0)×100`. |
| D-156 | `SecondaryLength` is not automatically equivalent to `Lu`. |
| D-157 | Graph Correction is a separate pipeline from mechanical-result calculation. |
| D-158 | Raw TXT data is never overwritten by Graph Correction. |
| D-159 | Horizontal-axis correction is the primary correction defined here. |
| D-160 | Stress/Force values are not changed solely by Graph Correction. |
| D-161 | FractureIndex remains a raw/analysis data location independent of corrected coordinates. |
| D-162 | Changing SecondaryLength recalculates the corrected graph representation. |
| D-163 | Changing SecondaryLength alone does not change Elongation After Fracture. |
| D-164 | OriginalDataset and CorrectedDataset remain separate. |
| D-165 | Corrected export includes correction provenance. |
| D-166 | All TB-010 calculations are array-based. |
| D-167 | Graph pixels are never a source of numerical results. |
| D-168 | Missing required Lu produces NOT_AVAILABLE. |
| D-169 | Missing/invalid required SecondaryLength produces NOT_AVAILABLE/INVALID for Graph Correction. |
| D-170 | Manual Graph Correction is recorded as an Event. |

## 32. Deferred Standard-Specific Rules

The following remain deferred until verified against the authorized ISO 6892-1 implementation text and actual project files:

- exact final gauge-length measurement procedure;
- specimen reassembly/alignment requirements;
- exact marking and measurement requirements;
- exact applicability of post-fracture elongation to specimen configurations;
- exact mapping of SecondaryLength to the graph-correction reference length;
- exact horizontal-axis correction equation;
- exact interaction between graph correction and modulus verification;
- detailed reporting requirements.

## 33. Next Blueprint

**TB-011 — ISO 6892-1 Young's Modulus / Elastic Region Selection & Horizontal Axis Correction Methodology**
