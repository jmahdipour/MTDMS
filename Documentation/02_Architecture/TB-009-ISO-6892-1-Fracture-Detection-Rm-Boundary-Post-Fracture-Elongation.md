# TB-009 — ISO 6892-1 Fracture Detection, Rm Boundary & Post-Fracture Elongation Specification

**Document:** TB-009  
**Project:** MTDMS — Material Test Data Management System  
**Version:** 1.0  
**Status:** Draft for Approval  
**Parent:** TB-007, TB-008, TB-008.1  
**Standard:** ISO 6892-1:2019  
**Scope:** Output TXT file analysis only  
**Calculation model:** Array-Based

## 1. Purpose

TB-009 defines the data-analysis contract for:

- maximum force / tensile strength boundary;
- fracture detection;
- separation of fracture from extensometer release;
- post-fracture elongation calculation;
- traceability of fracture-related events.

The document does not control the testing machine or acquisition hardware.

## 2. Fundamental Separation

The following are independent events/results:

```text
Extensometer Attach
Yield / Proof Strength
Maximum Force / Rm
Extensometer Release
Fracture
Post-Fracture Elongation
```

In particular:

```text
Extensometer Release ≠ Fracture
Rm ≠ Fracture
```

## 3. Rm Definition in MTDMS

The maximum tensile stress result is derived from the maximum valid tensile force in the test dataset and the original cross-sectional area:

```text
Fm = Maximum Valid Force
Rm = Fm / A0
```

The corresponding sample index is retained:

```text
RmIndex
RmTime
RmDisplacement
RmSource
```

The exact standard-specific validity/filtering rules for identifying `Fm` must follow the authorized ISO 6892-1 implementation text.

## 4. Maximum-Force Boundary

The engine identifies the maximum valid force using the calculated Force array, not the graph image.

```text
ForceN()
   ↓
Valid Test Range
   ↓
Maximum Valid Force
   ↓
FmIndex
```

The raw Force array is never modified.

## 5. Local Maximum vs Noise

A single noisy spike must not automatically be accepted as the physical maximum force.

The engine must distinguish:

```text
CandidateMaximum
ValidatedMaximum
```

Noise filtering and smoothing thresholds remain Method Configuration items until validated against the authorized standard implementation and real project files.

## 6. Fracture Event

Fracture is modeled independently as:

```text
FractureEvent
```

with at minimum:

```text
EventID
Index
Time
Displacement
Force
StrainSource
DetectionMethod
Status
Confidence
OperatorConfirmation
Provenance
```

## 7. Fracture Is Not Simply Last Row

The last row of the TXT file must not automatically be classified as fracture.

```text
LastIndex ≠ FractureIndex
```

The dataset may contain samples after the physical fracture or after a machine-side stop condition.

## 8. Fracture Detection Evidence

Fracture detection may use multiple independent indicators:

```text
Force drop
Post-maximum force behavior
Displacement progression
Extensometer behavior
Data continuity
Final elongation information
```

The automatic engine produces a candidate first.

```text
AUTO_CANDIDATE
```

Operator confirmation may subsequently produce:

```text
MANUAL_CONFIRMED
```

## 9. Force-Drop Candidate

A sudden force reduction after the maximum-force region is a fracture candidate.

Conceptually:

```text
Fm
 │
 │
 └───────┐
         │
         ▼
      Force Drop
         │
         ▼
   Fracture Candidate
```

A force drop alone is not sufficient for universal confirmation because other test/data events may also create force reductions.

## 10. Rm and Fracture Ordering

The normal tensile-test sequence is:

```text
Elastic Region
   ↓
Yield / Proof Region
   ↓
Plastic Region
   ↓
Fm / Rm
   ↓
Necking / Post-Fm Region
   ↓
Fracture
```

The data model must not hard-code this sequence as an assumption. It must validate the actual dataset.

## 11. Extensometer Release vs Fracture

The expected case may be:

```text
Rp0.2
  ↓
Extensometer Release
  ↓
Fm / Rm
  ↓
Fracture
```

Therefore the Release Event must not terminate the analysis.

## 12. Fracture Before Extensometer Release

The data model must also support:

```text
Extensometer active
       ↓
Fracture
       ↓
Extensometer Release / Data termination
```

If this occurs, the engine records the actual Event ordering rather than forcing Release before Fracture.

## 13. Fracture Candidate Window

The engine may define a candidate search window around the post-maximum region:

```text
FmIndex
   ↓
PostMaximumWindow
   ↓
ForceDropCandidates
```

The window size and force-drop criteria remain configurable and are not frozen here without validation against the authorized method and actual files.

## 14. Candidate Ranking

When several fracture candidates exist, the engine retains all candidates:

```text
FractureCandidates()
```

and separately records:

```text
SelectedFracture
```

No candidate is silently deleted.

## 15. Manual Fracture Selection

Graph Analysis may allow the operator to select the fracture location manually.

The operator selects the data location, not a report-only number.

After selection:

```text
SelectedFractureIndex
        ↓
Recalculate dependent results
```

## 16. Manual Fracture Event

```text
ManualFractureSelectionEvent
├── EventID
├── Index
├── PreviousCandidate
├── NewSelection
├── Reason
├── Operator
├── Timestamp
└── Comment
```

The original automatic candidate remains in provenance.

## 17. Post-Fracture Elongation

Post-fracture elongation is a physical/measured result and must not be confused with the instantaneous strain at the final machine sample.

The result should be based on the applicable ISO 6892-1 measurement procedure and the operator's measured final gauge length after fracture where required.

The project already requires support for operator-entered secondary/final length measurement.

## 18. L0 and Final Gauge Length

The original gauge length:

```text
L0
```

is retained separately from the measured final gauge length:

```text
Lu
```

The post-fracture elongation is conceptually:

```text
A = ((Lu - L0) / L0) × 100
```

The exact specimen preparation, fitting/alignment, and validity requirements must follow the authorized ISO 6892-1:2019 implementation text.

## 19. Operator Measurement

The operator may enter:

```text
FinalGaugeLength = Lu
```

This value is a measured post-test quantity and must have provenance:

```text
MeasuredBy
Timestamp
Unit
Operator
```

It must not overwrite `L0`.

## 20. Secondary Length

The project's graph-correction workflow also uses a manually measured secondary length for horizontal-axis scaling.

This is a separate concept from the post-fracture measured final gauge length unless the approved method explicitly maps the two.

Therefore:

```text
SecondaryLength ≠ automatically Lu
```

and:

```text
L0 ≠ automatically SecondaryLength
```

## 21. Horizontal Graph Scaling

Graph correction may use operator-measured secondary length to correct the horizontal strain representation.

The corrected visualization pipeline is:

```text
Raw Data
   ↓
Calculated Strain
   ↓
Graph Correction
   ↓
Corrected Strain Axis
```

This correction must not silently modify the Raw Dataset.

## 22. Post-Fracture Strain vs Post-Fracture Elongation

These are separate:

```text
FinalDataStrain
```

is a calculated data quantity, while:

```text
PostFractureElongation A
```

is based on the applicable final gauge-length measurement procedure.

Therefore the engine must not calculate `A` simply by taking the last strain sample unless the configured method explicitly permits it.

## 23. Fracture and Final Data Sample

The following can differ:

```text
FractureIndex
LastDataIndex
```

Example:

```text
FractureIndex = 4872
LastDataIndex = 4905
```

The post-fracture samples remain in Raw Data but are not automatically treated as additional tensile deformation after physical fracture.

## 24. True Stress / True Strain

True stress/strain calculations are separate from fracture detection.

```text
FractureDetection
        ↓
FractureIndex
        ↓
True Stress/Strain Method
```

The fracture Event must not be inferred from the true-strain calculation itself.

## 25. Result Structure

```text
FractureResult
├── FractureIndex
├── Time
├── Displacement
├── Force
├── StrainSource
├── DetectionMethod
├── Status
├── Confidence
├── OperatorConfirmation
└── Provenance
```

```text
RmResult
├── Fm
├── Rm
├── RmIndex
├── Time
├── A0
├── Source
├── Status
└── Provenance
```

```text
PostFractureElongationResult
├── L0
├── Lu
├── ElongationPercent
├── MeasurementMethod
├── Operator
├── Timestamp
├── Status
└── Provenance
```

## 26. Result Dependencies

```text
Fm / Rm
   │
   └── depends on valid maximum-force selection

Fracture
   │
   └── independent Event

Post-Fracture Elongation
   │
   └── depends on applicable final gauge-length measurement
```

Changing the fracture index must not automatically change `Rm` unless the approved maximum-force validation method makes the two results dependent.

## 27. Validation States

Possible states:

```text
VALID
WARNING
INVALID
NOT_AVAILABLE
AUTO_CANDIDATE
MANUAL_CONFIRMED
```

## 28. No Fracture Candidate

If the engine cannot establish a valid fracture candidate:

```text
Fracture.Status = NOT_AVAILABLE
```

It must not fabricate a fracture at `LastDataIndex`.

## 29. No Final Gauge Length

If the applicable post-fracture elongation method requires `Lu` and the operator has not supplied it:

```text
Elongation.Status = NOT_AVAILABLE
```

The engine must not silently substitute a calculated final strain.

## 30. Graph Analysis Display

Graph Analysis may display:

```text
Stress-Strain Curve
Fm / Rm Marker
Fracture Candidate
Selected Fracture
Extensometer Release
Post-Fracture Region
```

These markers are analysis aids and are not automatically included in the final report.

## 31. Final Report

The final report should contain the approved result values, not temporary candidate markers.

Potential reported results:

```text
Rm
Fm
Fracture Status
Elongation After Fracture
L0
Lu
```

The detailed candidate history remains available in the Dataset/Provenance layer.

## 32. Array-Based Traceability

All calculations are traceable to array indices:

```text
ForceN()
Displacement()
Deformationt()
EngineeringStress()
EngineeringStrain()
StrainSourceMap()
```

No fracture or Rm result is determined from chart pixels.

## 33. Freeze Decisions Proposed

| ID | Decision |
|---|---|
| D-135 | Rm/Fm and Fracture are independent results/events. |
| D-136 | Extensometer Release is independent from Fracture. |
| D-137 | Last TXT row is not automatically the fracture point. |
| D-138 | Rm is calculated from the validated maximum-force point and A0. |
| D-139 | Maximum-force selection is array-based. |
| D-140 | Fracture detection may create candidates before confirmation. |
| D-141 | Multiple fracture candidates are retained for traceability. |
| D-142 | Manual fracture selection is an Event. |
| D-143 | Automatic fracture candidates are never silently discarded. |
| D-144 | L0 and Lu are separate parameters. |
| D-145 | Post-fracture elongation is not automatically taken from the last strain sample. |
| D-146 | Operator-measured final gauge length has provenance. |
| D-147 | Secondary graph-correction length is separate from Lu unless explicitly mapped by the approved method. |
| D-148 | Graph correction does not modify Raw TXT data. |
| D-149 | Raw samples after the physical fracture remain retained. |
| D-150 | True stress/strain calculations do not define fracture by themselves. |
| D-151 | No fracture candidate produces NOT_AVAILABLE rather than a fabricated last-row fracture. |
| D-152 | Missing required Lu produces NOT_AVAILABLE for post-fracture elongation. |

## 34. Deferred Rules

The following require verification against the authorized ISO 6892-1:2019 implementation text and project test files before final Freeze:

- exact fracture-detection threshold;
- exact force-drop criterion;
- noise filtering/smoothing rules;
- exact selection window after Fm;
- treatment of multiple local maxima;
- exact requirements for final gauge-length measurement;
- specimen reassembly/alignment requirements;
- exact applicability of post-fracture elongation measurement to each specimen type;
- exact reporting rules for fracture location.

## 35. Next Blueprint

**TB-010 — ISO 6892-1 Elongation After Fracture, Gauge-Length Measurement & Horizontal Axis Correction Specification**
