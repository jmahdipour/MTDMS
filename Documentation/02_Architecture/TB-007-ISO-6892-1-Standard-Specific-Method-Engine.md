# TB-007 — Standard-Specific Method Engine: ISO 6892-1

**Document:** TB-007  
**Project:** MTDMS — Material Test Data Management System  
**Version:** 1.0  
**Status:** Approved / Frozen  
**Standard:** ISO 6892-1:2019  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in  
**Calculation model:** Array-Based

## 1. Purpose

TB-007 defines the Standard-specific Method Engine contract for ISO 6892-1 analysis of metallic tensile-test output files.

```text
TXT
 ↓
Dataset
 ↓
ISO 6892-1 Method Engine
 ↓
Stress / Strain
 ↓
Elastic Region
 ↓
Proof Strength / Yield
 ↓
Rm
 ↓
Fracture
 ↓
Elongation
 ↓
Graph Correction
```

## 2. Scope Boundary

MTDMS analyzes the exported TXT file only. It does not control the testing machine, PLC, drive, crosshead, extensometer, test speed, or real-time acquisition.

If information required by ISO 6892-1 is not present in the TXT file or supplied as an approved test input, MTDMS must report `UNKNOWN`, `NOT_AVAILABLE`, or a validation warning rather than inventing a value.

## 3. Input Contract

The approved file structure supplies the following metadata fields for the current project scope:

```text
Metadata
├── d/a    ← line 10
├── b      ← line 11
└── L0     ← line 13
```

Data columns:

```text
No
Time
Displacement
Deformationt
Force
```

Force is exported in `kgf`.

`Deformationt` is populated when extensometer data is available.

## 4. Array-Based Principle

All calculations operate on arrays. Raw input is never overwritten.

```text
ForceRaw()
ForceN()
CrossheadStrain()
ExtensometerStrain()
EngineeringStrain()
EngineeringStress()
CorrectedStrain()
StrainSource()
```

## 5. Force Conversion

Raw force remains in kgf:

```text
ForceRaw(i) = kgf
```

For SI calculations:

```text
ForceN(i) = ForceRaw(i) × 9.80665
```

`ForceRaw()` and `ForceN()` remain separate arrays.

## 6. Engineering Stress

After initial cross-sectional area `A0` is available:

```text
EngineeringStress(i) = ForceN(i) / A0
```

With Force in N and Area in mm², stress is MPa.

## 7. Strain Source Policy

The approved default source is Crosshead:

```text
Initial Source = CROSSHEAD
```

The operator may manually switch to Extensometer. The source may later switch back to Crosshead after the independent Extensometer Release Event.

Conceptually:

```text
CROSSHEAD
     ↓
EXTENSOMETER
     ↓
CROSSHEAD
```

The Method Engine consumes `StrainSource()` and does not silently replace the configured source.

## 8. Crosshead Strain

Where Crosshead is the active source:

```text
εCH(i) = ΔLCH(i) / L0
```

The displacement origin/zero must be defined by the analysis configuration; the Method Engine must not silently assume an origin when the dataset does not establish one.

## 9. Extensometer Strain

Where Extensometer is active and valid:

```text
εEXT(i) = Deformationt(i) / L0
```

`Deformationt()` remains raw input data and is not overwritten.

## 10. Extensometer Release

`ExtensometerReleasePoint` is an independent Event.

```text
YieldPoint ≠ ExtensometerReleasePoint
ExtensometerReleasePoint ≠ FracturePoint
```

If the release cannot be established from the file or manual operator action, it must remain unresolved rather than being inferred as a fact.

## 11. Young's Modulus

Young's modulus is an independent calculated result based on an approved elastic-region regression:

```text
Stress = E × Strain + b
```

Result structure:

```text
YoungModulus
├── Value
├── Unit
├── StartIndex
├── EndIndex
├── R²
├── Intercept
├── StrainSource
└── Method
```

## 12. Elastic Region

The Method Engine evaluates continuous candidate regions rather than assuming the first data points are automatically the elastic region.

Candidate selection may consider:

```text
R²
PointCount
StrainRange
StressRange
Continuity
StrainSource
Standard constraints
```

No universal R² threshold is frozen by TB-007 without the applicable standard text/method specification.

## 13. Proof Strength

For materials/methods where a conventional yield point is not applicable, the Method Engine supports Proof Strength methods such as configured offsets.

Conceptual structure:

```text
ProofStrengthMethod
├── Offset
├── ElasticModulus
├── ReferenceStrain
├── ResultStress
├── ResultStrain
├── IntersectionIndex
└── Method
```

## 14. Rp0.2

When the configured method is `Rp0.2`, the offset is 0.002 engineering strain.

The offset line uses the approved elastic slope and is intersected with the measured Stress-Strain curve.

Conceptually:

```text
σoffset(ε) = E × (ε - 0.002) + b
```

The exact standard-specific construction, validity range, tolerances, and reporting rules must be taken from the authorized ISO 6892-1:2019 implementation specification before numerical rules are independently frozen.

## 15. Array-Based Intersection

The Proof Strength intersection is determined from arrays, not from a rendered graph image.

```text
Difference(i) = EngineeringStress(i) - OffsetStress(i)
```

A sign transition or approved intersection condition identifies the surrounding points.

## 16. Interpolation

If the intersection occurs between two samples, the Method Engine may interpolate the intersection according to the approved method rather than simply selecting one raw sample.

Result retains:

```text
ProofStrengthResult
├── Stress
├── Strain
├── Interpolated
├── LowerIndex
└── UpperIndex
```

Exact interpolation requirements remain Standard-specific.

## 17. Yield Point vs Proof Strength

These are distinct result types:

```text
YieldPoint
ProofStrength
```

Examples of configured methods may include:

```text
YIELD_POINT
RP0.2
RP0.1
RP0.5
```

The selected method must be explicit in the analysis configuration.

## 18. Rm / UTS

Maximum Engineering Stress in the valid test range is the basis for `Rm`:

```text
Rm = Max(EngineeringStress())
```

The corresponding index and related values are retained:

```text
Rm
RmIndex
RmTime
RmStrain
RmForce
```

## 19. Fracture

Fracture is an independent Event and is not equivalent to Rm.

Normally:

```text
RmIndex < FractureIndex
```

may occur.

A force/stress drop is a fracture candidate, not automatically a confirmed fracture.

Potential non-fracture causes include:

```text
Noise
Temporary Force Drop
Grip Slip
Sampling Spike
Extensometer Release
Machine Pause
```

## 20. Fracture Validation

Conceptual sequence:

```text
Candidate
   ↓
Local Data Check
   ↓
Force/Stress Drop Check
   ↓
Post-Drop Behavior
   ↓
Operator Verification
```

The exact numerical fracture-detection rule is Standard-specific and remains configurable.

## 21. Graph Cut

The normal final engineering test graph terminates at the confirmed `FracturePoint`.

Post-fracture raw samples remain in the Dataset for traceability but are not displayed as part of the normal final test curve unless a separate approved analysis requires them.

## 22. Elongation After Fracture

Post-fracture gauge length is represented by `L2` / `SecondaryLength`.

```text
L0 = Original Gauge Length
L2 = Measured Final Gauge Length
```

The elongation result is:

```text
A% = ((L2 - L0) / L0) × 100
```

This result is independent of the graph's instantaneous strain value at `FractureIndex`.

## 23. Fracture Strain vs Elongation

The following are separate concepts:

```text
FractureStrain
ElongationAfterFracture
```

Conceptually:

```text
FractureStrain = EngineeringStrain(FractureIndex)

ElongationAfterFracture = ((L2-L0)/L0) × 100
```

The first is a dataset/graph quantity; the second is based on the post-fracture physical measurement.

## 24. Horizontal Graph Correction

Graph Correction may use approved inputs including:

```text
L0
L2
YoungModulus
YieldPoint
FracturePoint
EngineeringStrain()
```

It produces a separate array:

```text
CorrectedStrain()
```

The calculated dataset is never overwritten.

## 25. Graph Correction Philosophy

Graph Correction is a corrected visualization layer, not a modification of the raw test record.

```text
RawStrain ≠ CorrectedStrain
```

Both remain traceable.

## 26. Young's Modulus and Graph Correction

Where an approved correction method uses a reference/target modulus:

```text
Measured Elastic Slope
        ↓
Reference/Target Modulus
        ↓
Horizontal Axis Correction
```

This does not replace or overwrite the measured `E_test` result.

## 27. Standard Method Configuration

Conceptual ISO configuration:

```text
ISO6892_1_Method
├── TestMethod
├── ProofStrengthType
├── Offset
├── ElasticRegionMethod
├── StrainSourcePolicy
├── FractureMethod
├── GraphCutPolicy
└── ValidationRules
```

## 28. Test Method Metadata

Where applicable, the Method Engine can retain a configured test method such as:

```text
A1
A2
B
```

However, because MTDMS analyzes the output file only, the system must not infer a method that is not supported by the file or approved test configuration.

If the TXT cannot establish the method:

```text
TestMethod = UNKNOWN
```

## 29. Temperature

If temperature information exists in the source file or approved test metadata, it may be validated against the applicable ISO 6892-1 requirements.

If it does not exist:

```text
Temperature = NOT_AVAILABLE
```

No default temperature is invented.

## 30. Validation Levels

```text
LEVEL 1 — Dataset Integrity
LEVEL 2 — ISO Calculation Validity
LEVEL 3 — Report / Graph Validity
```

Examples:

```text
LEVEL 1
✓ Numeric arrays valid
✓ Array lengths consistent
✓ No invalid indexes

LEVEL 2
✓ A0 available
✓ L0 available
✓ Valid strain source
✓ Valid modulus region

LEVEL 3
✓ Fracture status established
✓ Graph ends at fracture
✓ Correction provenance available
```

## 31. Result Status

Each calculated result may have:

```text
VALID
WARNING
INVALID
NOT_AVAILABLE
MANUAL
```

If required input is absent, `NOT_AVAILABLE` is preferred to a fabricated numerical result.

## 32. Missing Extensometer Data

If `Deformationt()` contains no valid extensometer data, MTDMS must not assume that an extensometer was connected merely because the column exists.

The status becomes:

```text
ExtensometerDataStatus = NOT_AVAILABLE
```

and the valid source remains Crosshead unless a verified manual Event says otherwise.

## 33. Extensometer Release and Zero Deformation

A transition such as:

```text
Deformationt → 0
```

may be a release candidate, but it is not by itself proof of release.

It must be represented as an Auto Candidate or Manual Confirmed Event according to the configured workflow.

## 34. ISO6892Result

The Method Engine produces conceptually:

```text
ISO6892Result
│
├── A0
├── L0
├── YoungModulus
├── Yield
├── ProofStrength
├── Rm
├── RmIndex
├── FracturePoint
├── ElongationAfterFracture
├── StrainSourceSegments
├── Validation
└── Provenance
```

## 35. Traceability

Every result must be traceable to source data and method configuration.

For example:

```text
Rp0.2
│
├── Dataset
├── StartIndex
├── EndIndex
├── YoungModulus
├── Offset = 0.002
├── Intersection
├── Method
└── CalculationVersion
```

## 36. Explicitly Deferred Numerical Rules

The following must not be falsely represented as frozen ISO requirements without the authorized standard text/implementation specification:

- exact elastic-regression ranges;
- universal R² acceptance threshold;
- detailed strain-rate rules when the required acquisition metadata is absent;
- exact tolerances;
- detailed extensometer validity rules;
- detailed proof-strength construction rules beyond the configured method concept;
- detailed interpolation requirements;
- exact automatic fracture-detection thresholds.

These will be defined in the corresponding Standard-specific calculation specifications.

## 37. Approved Design Decisions

| ID | Decision |
|---|---|
| D-80 | ISO 6892-1 Method Engine is independent of Parser and Dataset. |
| D-81 | MTDMS does not control machine, PLC, drive, or real-time acquisition. |
| D-82 | Raw kgf Force is preserved and ForceN is a separate calculation array. |
| D-83 | Engineering Stress is calculated as an independent array. |
| D-84 | Initial strain source is Crosshead. |
| D-85 | Extensometer may be manually activated. |
| D-86 | Extensometer Release is an independent Event. |
| D-87 | Yield and Proof Strength are distinct methods/results. |
| D-88 | Rp0.2 uses the configured 0.002 offset concept and approved elastic slope. |
| D-89 | Rm is based on maximum Engineering Stress within the valid test range. |
| D-90 | Rm and Fracture Point remain independent. |
| D-91 | Normal final graph terminates at Fracture Point. |
| D-92 | L2 is used for Post-Fracture Elongation. |
| D-93 | L2 does not replace L0. |
| D-94 | Graph Correction creates a new data layer. |
| D-95 | Test Method is recorded only when supported by source/configuration. |
| D-96 | Missing required information is reported as UNKNOWN/NOT_AVAILABLE rather than guessed. |
| D-97 | Exact numerical ISO rules are not frozen without the authorized standard text/implementation specification. |
| D-98 | ISO 6892-1 Method Engine is extensible and independent from other standards. |

## 38. Next Blueprint

**TB-008 — ISO 6892-1 Proof Strength / Rp0.2 Calculation Specification**

TB-008 will define the numerical array-based specification for Rp0.2, Offset Line construction, intersection detection, interpolation, and interaction with the Crosshead/Extensometer strain-source segmentation.
