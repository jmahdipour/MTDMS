# TB-006 — Yield Detection, Fracture Detection & Graph Analysis Methodology

**Document:** TB-006  
**Project:** MTDMS — Material Test Data Management System  
**Version:** 1.0  
**Status:** Approved / Frozen  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in  
**Calculation model:** Array-Based

## 1. Purpose

TB-006 defines the engineering analysis methodology for elastic-region identification, Young's modulus, Yield Point, Fracture Point, Material Library assistance, operator verification, and Graph Correction.

The pipeline is:

```text
Raw Dataset
     ↓
Force Conversion
     ↓
Stress / Strain Arrays
     ↓
Elastic Region Analysis
     ↓
Young's Modulus
     ↓
Yield Candidate
     ↓
Operator Verification
     ↓
Final Yield
     ↓
Fracture Analysis
     ↓
Final Fracture
     ↓
Graph Correction
```

No result may be based only on a single point without the applicable analysis context.

## 2. Input Arrays

Primary arrays:

```text
No()
Time()
Displacement()
Deformationt()
ForceRaw()
ForceN()
EngineeringStress()
CrossheadStrain()
ExtensometerStrain()
EngineeringStrain()
StrainSource()
```

Primary Events:

```text
YieldPoint
ExtensometerStartPoint
ExtensometerReleasePoint
FracturePoint
```

## 3. Elastic Region

Young's modulus is calculated from a selected region whose Stress-Strain behavior is approximately linear.

The system must not blindly assume that the first points constitute the elastic region.

An `ElasticCandidate` contains:

```text
StartIndex
EndIndex
StrainSource
StressRange
StrainRange
Status
```

## 4. Linear Regression

For each candidate region:

```text
Stress = E × Strain + b
```

The result retains:

```text
E
Intercept
R²
StartIndex
EndIndex
PointCount
StrainSource
CalculationMethod
```

R² is an indicator of linear fit quality, not the sole selection criterion.

## 5. Elastic Region Selection

Candidate selection considers, as applicable:

```text
R²
PointCount
StrainRange
StressRange
Continuity
StrainSource
```

The longest geometric line, highest R², or largest point count alone is insufficient as a universal selection rule.

The final selection rule is configurable by the applicable Standard/Test Method.

## 6. Material Library

Material Library may provide:

```text
E_reference
ExpectedYield
```

It may assist in defining a candidate region or plausibility check.

It does not replace the measured test result unless an explicitly approved standard-specific method requires such use.

## 7. Young's Modulus Reference Comparison

Where a reference modulus exists, the analysis may report:

```text
E_test
E_reference
Difference
DifferencePercent
```

`E_reference` must not silently overwrite `E_test`.

## 8. Yield Detection

Yield detection supports:

```text
AUTO
MANUAL
LIBRARY_ASSISTED
```

The detailed numerical method is Standard-specific and is not globally frozen by TB-006.

The output includes:

```text
YieldPoint
YieldStress
YieldStrain
DetectionMethod
Confidence
OperatorConfirmed
```

## 9. Manual Yield Selection

Graph Analysis permits operator selection of Yield Point where the approved method allows manual verification.

Example:

```text
Automatic Index = 1850
Operator Index  = 1872
```

The final result uses the confirmed value and preserves the previous value in Event History.

## 10. Library-Assisted Yield Search

Material Library may define an expected yield region:

```text
ExpectedYield
      ↓
Candidate Window
      ↓
Dataset Points
      ↓
Automatic / Manual Selection
      ↓
YieldPoint
```

A range such as ±20% may be configured where appropriate, but ±20% is not a universal frozen rule.

## 11. Yield Search Window

Conceptual structure:

```text
YieldSearchWindow
├── Center
├── LowerBound
├── UpperBound
├── Source
├── Configuration
└── Method
```

The window is a search aid and is not itself the Yield result.

## 12. Yield and Extensometer Release

Yield and extensometer release remain independent:

```text
YieldIndex ≠ ExtensometerReleaseIndex
```

Yield may occur before or after extensometer release. The analysis engine must support both states and validate them against the applicable test method.

## 13. Fracture Detection

Fracture analysis must be context-based.

A significant force/stress drop can be a fracture candidate, but the first drop is not automatically fracture.

Potential non-fracture causes include:

```text
Noise
Temporary Force Drop
Grip Slip
Sampling Spike
Extensometer Release
Machine Pause
```

## 14. Fracture Candidate

Conceptual structure:

```text
FractureCandidate
├── Index
├── PreviousForce
├── CurrentForce
├── DropMagnitude
├── DropPercent
├── Stress
├── Strain
└── Confidence
```

Candidate detection must be followed by validation or operator confirmation according to the configured method.

## 15. Fracture Validation

Conceptual sequence:

```text
Candidate
   ↓
Local Data Check
   ↓
Force Drop Check
   ↓
Post-Drop Behavior
   ↓
Operator Verification
```

## 16. Fracture Search Range

Fracture is searched only within the meaningful loading/test range defined by the applicable method.

The final graph must not continue the test curve beyond the confirmed Fracture Point unless a separate analysis explicitly requires post-fracture data.

## 17. Operator Fracture Verification

Graph Analysis permits manual selection where approved:

```text
Click Point
    ↓
Fracture Candidate
    ↓
Confirm
    ↓
FracturePoint
```

## 18. Confidence

Automatic Event results may retain:

```text
HIGH
MEDIUM
LOW
```

Confidence supports review and workflow decisions but does not replace required operator confirmation.

## 19. Analysis Order

The approved conceptual order is:

```text
1. Dataset Validation
2. Source Segmentation
3. Elastic Region
4. Young's Modulus
5. Yield Candidate
6. Yield Verification
7. Fracture Candidate
8. Fracture Verification
9. Final Engineering Results
10. Graph Correction
```

## 20. Graph Analysis

Graph Analysis is a distinct stage between calculation and final visualization.

```text
Calculated Dataset
        ↓
Graph Analysis
        ↓
Operator Tools
        ↓
Verified Events
```

Operator tools may include:

- Yield Point selection/movement;
- Elastic Region review;
- Extensometer Start/Release review;
- Fracture Point selection;
- Material Library review;
- Regression-line visualization.

## 21. Regression Guide Line

The regression line used for elastic-region verification is an analysis/verification object.

It must not appear in the final report unless the applicable report specification requires it.

## 22. Largest Straight Line

The analysis may evaluate multiple continuous candidate regions.

Selection must not be based only on:

```text
Maximum R²
```

or only:

```text
Maximum PointCount
```

A configured method must consider fit quality, region size, continuity, strain range, and applicable standard constraints.

## 23. Horizontal Axis Graph Correction

Graph Correction may modify the displayed horizontal-axis strain using approved inputs including:

```text
L0
SecondaryLength (L2)
YoungModulus
YieldPoint
FracturePoint
EngineeringStrain()
```

The corrected visualization is stored separately, for example:

```text
CorrectedStrain()
```

Raw and calculated arrays remain unchanged.

## 24. Graph Correction Philosophy

Graph Correction is:

```text
Corrected Visualization
```

not:

```text
Modified Raw Test Result
```

Therefore:

```text
RawStrain ≠ CorrectedStrain
```

Both remain traceable.

## 25. Secondary Length

`SecondaryLength`/`L2` is a post-test measurement input, not an Event.

It contains at least:

```text
Value
Unit
Operator
Timestamp
MeasurementMethod
```

Post-fracture elongation is calculated as:

```text
A% = ((L2 - L0) / L0) × 100
```

## 26. Strain After Fracture

`EngineeringStrain(FractureIndex)` must not automatically be treated as Post-Fracture Elongation.

The latter is based on the measured post-fracture gauge length `L2` and original gauge length `L0`.

## 27. Graph Cut at Fracture

The final engineering test graph ends at the confirmed `FracturePoint`.

Post-fracture raw points remain in the Dataset for traceability but are excluded from the normal final test curve unless a separate analysis requires them.

## 28. Raw / Calculated / Corrected Layers

```text
RAW
  ↓
CALCULATED
  ↓
CORRECTED
```

Examples:

```text
ForceRaw()
EngineeringStress()
EngineeringStrain()
CorrectedStrain()
```

No layer overwrites the previous layer.

## 29. Manual Correction Provenance

Every manual Event correction records conceptually:

```text
EventType
OldIndex
NewIndex
OldValue
NewValue
Method = MANUAL
Operator
Timestamp
Reason
```

## 30. Final Event Object

Conceptual Event structure:

```text
Event
├── Type
├── Index
├── Time
├── Value
├── Source
├── Method
├── Confidence
├── OperatorConfirmed
└── Provenance
```

## 31. Method Engine Architecture

```text
Test Configuration
       │
       ├── Standard
       ├── Material
       ├── Yield Method
       ├── Geometry
       └── Strain Source
                │
                ▼
        Analysis Method Engine
                │
        ┌───────┼────────┐
        ▼       ▼        ▼
      Elastic  Yield   Fracture
      Engine   Engine   Engine
        │       │        │
        └───────┼────────┘
                ▼
          Event Engine
                │
                ▼
        Verified Results
```

This allows Standard-specific methods to be added without changing the Parser or Dataset architecture.

## 32. Output

The analysis result contains conceptually:

```text
AnalysisResult
│
├── ElasticRegion
├── YoungModulus
├── YieldPoint
├── UTS
├── FracturePoint
├── ExtensometerReleasePoint
├── StrainSegments
├── CorrectedStrain
└── PostFractureElongation
```

## 33. Explicitly Deferred Items

TB-006 does not globally freeze the exact numerical algorithms for:

- Yield detection;
- Extensometer release detection;
- Fracture detection.

Those methods must be defined and validated against the applicable Standard/Test Method.

MTDMS will not impose one universal Yield/Fracture algorithm on all materials and standards.

## 34. Approved Design Decisions

| ID | Decision |
|---|---|
| D-62 | Elastic Region is analyzed using regression. |
| D-63 | Young's Modulus is obtained from the regression slope. |
| D-64 | Material Library is Reference/Candidate Guidance only. |
| D-65 | Yield supports AUTO, MANUAL and LIBRARY_ASSISTED modes. |
| D-66 | Yield is independent from Extensometer Release. |
| D-67 | Fracture Detection is context-based. |
| D-68 | A single force drop does not automatically prove fracture. |
| D-69 | Fracture can be operator-confirmed. |
| D-70 | Automatic Event results may carry Confidence. |
| D-71 | Graph Analysis is separate from the Calculation Engine. |
| D-72 | Regression Guide Line is a verification object. |
| D-73 | Normal final graph ends at FracturePoint. |
| D-74 | Post-fracture raw data remains preserved. |
| D-75 | Graph Correction creates new visualization data and does not overwrite Raw/Calculated data. |
| D-76 | L2 is used for Post-Fracture Elongation. |
| D-77 | EngineeringStrain at fracture is not automatically equal to Post-Fracture Elongation. |
| D-78 | Yield/Fracture numerical methods are Standard-specific. |
| D-79 | No universal Yield/Fracture algorithm is imposed across all standards. |

## 35. Next Blueprint

**TB-007 — Standard-Specific Method Engine: ISO 6892-1**

TB-007 will define the first Standard-specific implementation contract for ISO 6892-1, including Rp0.2/Rt methods, elastic-region methodology, extensometer use, Yield determination, fracture handling, and the permitted boundary between calculated results and Graph Correction.

No application code is defined by TB-006.
