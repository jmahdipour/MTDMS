# TB-011 — ISO 6892-1 Young’s Modulus / Elastic Region Selection & Horizontal Axis Correction Methodology

**Document:** TB-011  
**Project:** MTDMS — Material Test Data Management System  
**Version:** 1.0  
**Status:** Approved / Frozen  
**Parent:** TB-007, TB-008, TB-008.1, TB-009, TB-010  
**Standard:** ISO 6892-1:2019  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in  
**Calculation model:** Array-Based

## 1. Purpose

TB-011 defines the analysis contract for:

1. selecting the elastic region;
2. calculating and validating elastic slope;
3. distinguishing elastic slope/mE from Young’s modulus/E;
4. using the approved elastic reference for horizontal-axis graph correction.

It applies only to exported TXT data and does not control the testing machine or acquisition hardware.

## 2. E and mE Separation

The data model keeps these results independent:

```text
ElasticSlope / mE
YoungsModulus / E
```

They are not automatically treated as identical.

## 3. Strain Source

The elastic analysis uses:

```text
EngineeringStress()
EngineeringStrain()
StrainSourceMap()
```

The project's normal source sequence is:

```text
CROSSHEAD → EXTENSOMETER → CROSSHEAD
```

## 4. Initial Source

Before a valid Extensometer Attach Event, the default strain source is:

```text
CROSSHEAD
```

## 5. Extensometer Attach

After a valid `ExtensometerAttachEvent`, the source map may switch to:

```text
EXTENSOMETER
```

according to the approved event state.

## 6. Extensometer Release

After a confirmed `ExtensometerReleaseEvent`, the source map may switch back to:

```text
CROSSHEAD
```

Release is independent from Yield, Rp0.2, Rm and Fracture.

## 7. Elastic Region Candidate

The engine creates one or more candidates rather than assuming that the first samples are elastic.

```text
ElasticRegionCandidate
├── StartIndex
├── EndIndex
├── Source
├── Slope
├── Intercept
├── R2
├── PointCount
├── StressRange
├── StrainRange
├── BoundaryCrossing
└── Stability
```

## 8. Initial Seating Region

The first data points may contain seating, settling, backlash or other non-representative behavior. Therefore:

```text
FirstDataPoint ≠ automatically ElasticRegionStart
```

Any exclusion rule is Method Configuration and must remain traceable.

## 9. Array-Based Regression

For a selected candidate:

```text
σ(i) = EngineeringStress(i)
ε(i) = EngineeringStrain(i)
```

The regression model is:

```text
σ = mε + c
```

with:

```text
m = ElasticSlope
c = Intercept
```

## 10. Regression Quality

Each candidate stores:

```text
Slope
Intercept
R2
PointCount
```

R² is a quality indicator but is not, by itself, sufficient to select the elastic region.

## 11. Multi-Criteria Selection

Candidate ranking may consider:

```text
Source consistency
Stress/strain range
Point count
R2
Slope stability
Distance from seating region
Distance from yield/proof region
Boundary crossing
```

Thresholds remain Method Configuration items.

## 12. Largest Straight Segment

The engine may identify the largest stable approximately linear segment as:

```text
LargestStraightSegment
```

This is an analysis candidate and is not automatically reported as Young’s modulus.

## 13. Source Boundary

A regression must not silently combine different strain sources.

Example:

```text
1–800       CROSSHEAD
801–1500    EXTENSOMETER
```

A regression spanning `700–1000` is:

```text
BoundaryCrossing = TRUE
```

and receives `WARNING` unless the configured method explicitly validates the common strain basis.

## 14. Manual Elastic Selection

Graph Analysis allows manual selection of:

```text
ElasticStartIndex
ElasticEndIndex
```

The mouse is only an interface for selecting Dataset indices. Calculations always use the underlying arrays.

## 15. Manual Selection Event

```text
ManualElasticRegionEvent
├── EventID
├── StartIndex
├── EndIndex
├── PreviousCandidate
├── NewSelection
├── Operator
├── Timestamp
├── Reason
└── Comment
```

Automatic candidates remain traceable after manual override.

## 16. Young’s Modulus

When the configured ISO 6892-1 method requires Young’s modulus, the dedicated Method Engine determines it.

The project must not derive E simply by copying the Rp0.2 slope calculation.

## 17. Material Library Reference

Material Library may provide:

```text
ExpectedYoungsModulus
```

for verification and graph-analysis purposes.

It does not automatically replace measured E.

## 18. Modulus Comparison

The system may calculate a comparison value:

```text
Deviation = (MeasuredE - ExpectedE) / ExpectedE × 100
```

Acceptance thresholds are Method Configuration values.

## 19. Horizontal Axis Correction

Graph correction is a separate visualization layer:

```text
OriginalStrain
      ↓
ElasticAnalysis
      ↓
MeasuredSlope / Reference
      ↓
CorrectionFactor
      ↓
CorrectedStrain()
```

Raw arrays remain unchanged.

## 20. Correction Factor

Where the configured method uses slope matching, the conceptual factor is:

```text
CorrectionFactor = ReferenceSlope / MeasuredSlope
```

and the corrected representation may be calculated as:

```text
CorrectedStrain(i) = OriginalStrain(i) × CorrectionFactor
```

The exact production equation remains Method Configuration until validated against the authorized implementation.

## 21. Reference Source

The correction reference may be supplied by:

```text
Material Library
Method Configuration
Approved Operator Reference
```

The selected reference and version must be stored in provenance.

## 22. Intercept

Regression retains both:

```text
m
c
```

because a high R² alone does not prove that the line is correctly positioned relative to the expected origin.

## 23. Zero Correction vs Slope Correction

These are independent operations:

```text
Zero/Origin Correction
Slope Correction
```

They must not be silently combined.

## 24. Correction Ordering

The approved pipeline is:

```text
Raw Data
   ↓
Event Engine
   ↓
Strain Source Map
   ↓
Engineering Strain
   ↓
Elastic Analysis
   ↓
Horizontal Axis Correction
```

Correction must occur after source segmentation.

## 25. Main Project Scenario

A valid test may contain:

```text
Elastic Region → EXTENSOMETER
Rp0.2          → EXTENSOMETER
Release        → CROSSHEAD
Rm             → CROSSHEAD
Fracture       → CROSSHEAD
```

The engine must support this without merging the source segments.

## 26. Elastic Region Before Extensometer

If the valid elastic region occurs before Extensometer attachment:

```text
ElasticSource = CROSSHEAD
```

unless the configured method explicitly provides a valid alternative.

## 27. Elastic Region Around Release

If an elastic candidate crosses the Release boundary, the engine records:

```text
BoundaryCrossing = TRUE
```

and applies the configured validation rule instead of silently merging the sources.

## 28. Graph Analysis Display

Analysis UI may display:

```text
Stress-Strain Curve
Elastic Candidate
Selected Elastic Region
Regression Line
Measured Slope
Measured E
Expected E
Yield
Rp0.2
Extensometer Release
```

These are analysis aids and are not automatically printed in the normal final report.

## 29. Report

Only approved results are reported, for example:

```text
Young’s Modulus
Elastic Slope / mE
```

according to the selected Method Configuration.

## 30. Provenance

```text
ElasticAnalysisProvenance
├── DatasetID
├── StartIndex
├── EndIndex
├── StrainSource
├── PointCount
├── Slope
├── Intercept
├── R2
├── SelectionMethod
├── Operator
├── Timestamp
└── CalculationVersion
```

Graph correction provenance includes:

```text
GraphCorrectionProvenance
├── SourceSlope
├── ReferenceSlope
├── CorrectionFactor
├── SourceDataset
├── CorrectedDataset
├── ReferenceSource
├── Method
└── Version
```

## 31. Validation States

```text
VALID
WARNING
INVALID
NOT_AVAILABLE
AUTO_CANDIDATE
MANUAL_CONFIRMED
MANUAL_REJECTED
BOUNDARY_CROSSING
```

## 32. Invalid/Unavailable Conditions

If no valid elastic candidate exists:

```text
ElasticSlope.Status = NOT_AVAILABLE
```

No artificial value is generated.

## 33. Array Outputs

The analysis layer may expose:

```text
EngineeringStress()
EngineeringStrain()
CorrectedStrain()
```

and results:

```text
ElasticSlope
MeasuredYoungsModulus
ExpectedYoungsModulus
R2
ElasticStartIndex
ElasticEndIndex
CorrectionFactor
```

## 34. Freeze Decisions

| ID | Decision |
|---|---|
| D-171 | `ElasticSlope/mE` and `YoungsModulus/E` are independent results. |
| D-172 | Elastic Region is selected from Array Data. |
| D-173 | Source Map is created before Elastic Analysis. |
| D-174 | Default initial strain source is Crosshead. |
| D-175 | Extensometer Attach and Release are independent Events. |
| D-176 | Regression must not silently combine different strain sources across a boundary. |
| D-177 | R² alone is insufficient for Elastic Region selection. |
| D-178 | Largest Straight Segment is an analysis candidate, not automatically Young’s modulus. |
| D-179 | Manual Elastic Region Selection is recorded as an Event. |
| D-180 | Automatic candidates remain traceable after manual override. |
| D-181 | Material Library Expected E does not automatically replace Measured E. |
| D-182 | Graph Correction is separate from the Raw Dataset. |
| D-183 | Graph Correction does not change Force/Stress values. |
| D-184 | Correction reference and factor are stored in provenance. |
| D-185 | Graph Correction follows Source Segmentation and Elastic Analysis. |
| D-186 | Numerical results are never extracted from graph pixels. |
| D-187 | No valid Elastic Region produces NOT_AVAILABLE. |
| D-188 | Candidate-quality thresholds remain Method-Specific and configurable. |

## 35. Deferred Standard-Specific Rules

The following remain Method Configuration items until verified against the authorized ISO 6892-1 implementation text and actual project files:

- exact elastic-region limits;
- exact regression interval;
- exact E determination procedure;
- exact correction equation;
- exact acceptance criteria;
- exact treatment of source boundaries;
- exact relationship between Material Library reference E and graph correction.

## 36. Next Blueprint

**TB-012 — ISO 6892-1 Stress/Strain Dataset Normalization, Units & Cross-Sectional Area Calculation Specification**
