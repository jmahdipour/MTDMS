# TB-022 — ISO 6892-1 Result Dependency Graph, Calculation Order & Recalculation Propagation Specification

**Document:** TB-022  
**Project:** MTDMS — Material Test Data Management System  
**Version:** 1.0  
**Status:** Approved / Frozen  
**Parent:** TB-018 → TB-019 → TB-020 → TB-021  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in  
**Calculation model:** Array-Based

## 1. Purpose

TB-022 defines the calculation order and dependency graph for MTDMS so that every Result is calculated only after its required dependencies are finalized, and changes propagate only to downstream dependent calculations.

## 2. Pipeline

```text
TXT File
   ↓
Import
   ↓
Raw Dataset
   ↓
Validation
   ↓
Normalization
   ↓
Test Start Boundary
   ↓
Strain Source Segmentation
   ↓
Engineering Stress
   ↓
Engineering Strain
   ↓
Valid Curve Dataset
   ↓
Yield / Rp Detection
   ↓
Rm
   ↓
Fracture Detection
   ↓
Fracture Finalization
   ↓
Post-Fracture Dataset
   ↓
Elongation After Fracture
   ↓
Graph Correction
   ↓
Final Results
   ↓
Report
```

## 3. Layer Separation

The analysis uses four logical layers:

```text
RAW
DERIVED
EVENT / BOUNDARY
RESULT
```

## 4. Raw Layer

The Raw Layer contains the values imported from the TXT file, including where available:

```text
Time
Force
Crosshead
Extensometer
OriginalRowIndex
```

Raw data is read-only for the analysis pipeline. Recalculation must never overwrite, sort, delete, or otherwise mutate the original TXT-derived values.

## 5. Derived Layer

The Derived Layer contains normalized and calculated arrays such as:

```text
NormalizedForce
Stress
CrossheadDisplacement
ExtensometerStrain
EngineeringStrain
```

## 6. Event / Boundary Layer

The Event/Boundary Layer includes:

```text
TestStart
ExtensometerAttach
ExtensometerRelease
Yield
Rp0.2
Rm
Fracture
CurveTerminal
```

## 7. Result Layer

The Result Layer includes, where applicable:

```text
YoungModulus
YieldStrength
Rp0.2
Rm
FractureStress
FractureStrain
ElongationAfterFracture
```

## 8. Dependency Graph

```text
RAW
 │
 ├── Force ───────────────┐
 │                         ↓
 │                    Stress
 │                         │
 │                         ↓
 │                  Valid Dataset
 │                         │
 ├── Crosshead ────────────┤
 │                         ↓
 │                  Strain Source
 │                         │
 └── Extensometer ─────────┘
                           │
                           ↓
                    Stress–Strain Curve
                           │
             ┌─────────────┼─────────────┐
             ↓             ↓             ↓
        Young Modulus    Yield/Rp        Rm
             │             │             │
             └─────────────┴──────┬──────┘
                                   ↓
                              Fracture
                                   ↓
                         Post-Fracture Boundary
                                   ↓
                         Elongation After Fracture
```

## 9. Mandatory Calculation Order

The logical calculation order is:

1. Import TXT.
2. Validate Raw Dataset.
3. Normalize units.
4. Validate cross-sectional area.
5. Calculate Engineering Stress.
6. Determine strain-source segmentation.
7. Calculate Engineering Strain.
8. Build the valid Stress–Strain Dataset.
9. Determine Young's Modulus / elastic region.
10. Detect Yield / Rp.
11. Determine Rm.
12. Detect Fracture.
13. Finalize Fracture Event.
14. Classify Post-Fracture Dataset.
15. Calculate Elongation After Fracture from physical gauge-length inputs.
16. Apply Graph Correction as a separate layer.
17. Produce final Results and Report.

## 10. Stress Dependencies

Stress depends on normalized Force and validated Cross-Sectional Area, including their units.

```text
Force
  +
Area
  ↓
Stress
```

## 11. Strain Dependencies

Engineering Strain depends on the selected strain source, initial gauge length and displacement data.

The strain source must be segmented before final Engineering Strain is generated.

## 12. Strain Source Segmentation

The approved project scenario permits:

```text
Extensometer
       ↓
Release Event
       ↓
Crosshead
```

The source switch is an independent Event and is not merged with Fracture.

## 13. Young's Modulus

Young's Modulus depends on:

```text
Valid Stress
Valid Strain
Elastic Region
```

It must not be calculated from an unvalidated region.

## 14. Yield / Rp

Yield and proof-strength calculations depend on the valid Stress–Strain Dataset and the applicable detection method. Rp0.2 additionally depends on the elastic reference line and the applicable 0.2% offset rule.

Where required, the applicable Extensometer Segment boundary defined by TB-008.1 must be respected.

## 15. Rm

Rm depends on the valid Engineering Stress Dataset and valid curve boundary.

```text
Rm = Maximum Valid Engineering Stress
```

The Rm calculation does not automatically define Fracture.

## 16. Fracture Detection

Fracture Detection depends on the validated Dataset and the applicable detection method. It may use Force, Stress, Strain, Rm/Post-Rm information and method-specific rules, but it must remain an independent Event from Rm and Extensometer Release.

## 17. Fracture Finalization

```text
Candidate Fracture
       ↓
Validation
       ↓
Operator Override (optional)
       ↓
FinalFractureIndex
```

## 18. Post-Fracture Dataset

The Post-Fracture classification is downstream of `FinalFractureIndex`:

```text
DatasetIndex > FinalFractureIndex
```

The fracture row itself remains in the Dataset.

## 19. Elongation After Fracture

Elongation After Fracture depends on physical measurement inputs:

```text
L0
L_after
Measurement Unit
```

where applicable:

```text
A% = ((L_after - L0) / L0) × 100
```

It is not calculated from the last Engineering Strain point.

## 20. Graph Correction

Graph Correction depends on the appropriate elastic reference, Young's Modulus, elastic-region selection, operator-provided secondary gauge length and the correction methodology.

Graph Correction must not overwrite Raw Dataset or silently modify the original Fracture boundary.

## 21. Result Dependency Graph

```text
                  ┌──────────────┐
                  │  RAW TXT     │
                  └──────┬───────┘
                         │
              ┌──────────┴──────────┐
              ↓                     ↓
        Force Normalize       Displacement
              │                     │
              ↓             ┌───────┴────────┐
          Stress             ↓                ↓
                         Extensometer      Crosshead
                              │                │
                              └───────┬────────┘
                                      ↓
                              Source Segmentation
                                      ↓
                              Engineering Strain
                                      │
                         ┌────────────┴────────────┐
                         ↓                         ↓
                    Valid Dataset              Stress
                         │
             ┌───────────┼───────────────┐
             ↓           ↓               ↓
           E-mod       Yield/Rp          Rm
             │           │               │
             └───────────┴───────┬───────┘
                                 ↓
                         Fracture Detection
                                 ↓
                         Fracture Finalization
                                 ↓
                        Post-Fracture Boundary
                                 │
                                 ↓
                     Elongation After Fracture
```

## 22. Recalculation Principle

A changed input must dirty only its downstream dependents rather than triggering an uncontrolled full recalculation.

## 23. Cross-Section Change

Changing Area affects, as applicable:

```text
Stress
 ↓
Valid Stress
 ↓
Young Modulus
 ↓
Yield / Rp
 ↓
Rm
 ↓
Fracture Stress
```

It does not change `L0` or `L_after`.

## 24. Initial Gauge Length Change

Changing `L0` affects Engineering Strain and downstream strain-dependent Results such as Young's Modulus, Yield/Rp and graph correction, as applicable.

It does not change Force or Stress.

## 25. Extensometer Release Change

Changing the Release Event can affect:

```text
Strain Source Segmentation
 ↓
Engineering Strain
 ↓
Young Modulus
 ↓
Yield / Rp
 ↓
Rm Strain
 ↓
Fracture Strain
```

It does not inherently change Force or Stress.

## 26. Rm Stress vs Rm Strain

A source-boundary change may leave `RmStress` unchanged while changing `RmStrain`. Dependencies must therefore be tracked at the Result level rather than assuming all Rm fields change together.

## 27. FractureIndex Change

Changing only `FinalFractureIndex` affects downstream boundary-dependent data such as:

```text
PostFractureFlag
CurveTerminal
Fracture Results
```

It must not change Young's Modulus, Rp0.2 or Rm unless the applicable Method explicitly defines such a dependency.

## 28. L_after Change

Changing only `L_after` affects:

```text
ElongationAfterFracture
Report
```

It does not change the Stress–Strain Dataset or fracture detection.

## 29. Graph Correction Change

Changing Secondary Gauge Length or Graph Correction parameters affects the corrected graph layer, not Raw Dataset. Any calculation result that explicitly depends on the corrected graph must be recalculated through its declared dependency.

## 30. Dependency Levels

```text
L0 = Raw
L1 = Normalized
L2 = Derived
L3 = Events / Boundaries
L4 = Results
L5 = Graph
L6 = Report
```

## 31. Upstream / Downstream Metadata

Each calculation node should expose:

```text
UpstreamDependencies
DownstreamDependents
```

Example:

```text
EngineeringStrain
Upstream:
    Crosshead
    Extensometer
    L0
    SourceBoundary

Downstream:
    YoungModulus
    Yield
    Rp0.2
    RmStrain
    FractureStrain
```

## 32. Dirty State

Calculation nodes support:

```text
CLEAN
DIRTY
INVALID
NOT_AVAILABLE
```

## 33. Dirty Propagation

```text
Input Changed
    ↓
Changed Node = DIRTY
    ↓
Downstream Nodes = DIRTY
```

Only required downstream nodes are recalculated.

## 34. Invalid Propagation

An invalid dependency must not produce a fabricated numeric Result.

Example:

```text
Stress = INVALID
       ↓
Rm = NOT_AVAILABLE
```

unless another explicitly defined valid Method provides the Result.

## 35. NOT_AVAILABLE vs Zero

`NOT_AVAILABLE` is not equivalent to zero.

Example:

```text
L_after = Missing
A%      = NOT_AVAILABLE
```

## 36. No Silent Fallback

The engine must not silently substitute one source or value for another, such as:

```text
Extensometer → Crosshead
Invalid → Zero
```

without an explicit rule, status and audit trail.

## 37. Recalculation Triggers

Supported trigger classes include:

```text
INPUT_CHANGE
CONFIG_CHANGE
METHOD_CHANGE
EVENT_OVERRIDE
GRAPH_CORRECTION
MEASUREMENT_CHANGE
```

## 38. Method Change

Changing the Standard Method invalidates/recalculates Method-specific Results and their declared downstream dependencies.

## 39. Configuration Change

Changes such as:

```text
Cross Section
Gauge Length
Material
Yield Method
Rp Offset
```

dirty only their declared downstream dependencies.

## 40. Material Library Change

Changing a Young's Modulus reference in the Material Library affects dependent graph-correction and analysis operations where that reference is used. It does not automatically alter Raw Data or independent Rm Stress.

## 41. Calculation Snapshot

A completed calculation should record:

```text
DatasetVersion
MethodVersion
ConfigurationVersion
CalculationVersion
```

## 42. Auditability

Every Result must be traceable to its source Dataset, Calculation Method, Configuration and relevant Event/Boundary decisions.

## 43. Result Status

Results may carry:

```text
VALID
INVALID
NOT_AVAILABLE
OVERRIDDEN
```

Automatic and Operator-derived values must remain auditable where override is supported.

## 44. Calculation Transaction

A logical analysis transaction follows:

```text
Load
 ↓
Validate
 ↓
Calculate
 ↓
Validate Results
 ↓
Commit Snapshot
```

A failed calculation must not silently replace a previous Valid Snapshot.

## 45. Calculation Engine Independence

The Calculation Engine must not depend on Ribbon UI state. The UI supplies configuration, inputs and explicit overrides; the analysis pipeline generates Results.

## 46. Graph Engine

The Graph Engine consumes declared Results and Derived arrays. It must not contain a second independent Stress/Strain calculation path.

## 47. Report Engine

The Report Engine consumes finalized Results and statuses. It must not independently recalculate Stress, Strain or other analytical Results.

## 48. Single Source of Truth

Each Result has one calculation owner:

| Result | Owner |
|---|---|
| Stress | Stress Engine |
| Engineering Strain | Strain Engine |
| Young Modulus | Elastic Analysis |
| Yield | Yield Engine |
| Rp0.2 | Proof Strength Engine |
| Rm | Rm Engine |
| Fracture | Fracture Engine |
| A% | Elongation Engine |
| Graph Corrected Strain | Graph Correction Engine |

## 49. Final Result Package

The final package contains:

```text
Dataset
Events
Boundaries
Results
Validation
Corrections
Audit
```

## 50. Freeze Decisions

| ID | Decision |
|---|---|
| D-426 | Calculation Pipeline has a deterministic logical order. |
| D-427 | Raw Dataset is never changed by Recalculation. |
| D-428 | Stress is calculated before dependent Results. |
| D-429 | Strain Source Segmentation is finalized before Engineering Strain. |
| D-430 | Engineering Strain precedes Young Modulus/Yield/Rp analysis. |
| D-431 | Valid Dataset is established before Rm. |
| D-432 | Fracture Detection is independent of Rm. |
| D-433 | Fracture Finalization precedes Post-Fracture classification. |
| D-434 | L_after is independent of Curve Dataset. |
| D-435 | A% is calculated from L0 and L_after. |
| D-436 | Graph Correction never overwrites Raw/primary calculation data. |
| D-437 | Input changes propagate only to downstream dependencies. |
| D-438 | Dirty propagation is auditable. |
| D-439 | Invalid dependencies do not produce fabricated numeric Results. |
| D-440 | NOT_AVAILABLE is distinct from zero. |
| D-441 | Source Switch and Fracture are independent Events. |
| D-442 | Method changes recalculate Method-specific Results. |
| D-443 | Material Library changes recalculate only declared dependent operations. |
| D-444 | Report Engine is not a calculation owner for analytical Results. |
| D-445 | Graph Engine is not a second Stress/Strain calculation owner. |
| D-446 | Every Result has one calculation owner. |
| D-447 | Automatic and Operator Override values remain auditable. |
| D-448 | Calculation Snapshots are versioned. |
| D-449 | Failed calculations do not overwrite the previous Valid Snapshot. |
| D-450 | DatasetVersion, MethodVersion, ConfigurationVersion and CalculationVersion are recorded. |
| D-451 | Single Source of Truth is mandatory for each Result. |
| D-452 | Final Result Package contains Dataset, Events, Boundaries, Results, Validation, Corrections and Audit. |

## 51. Status

**Approved / Frozen — TB-022.**
