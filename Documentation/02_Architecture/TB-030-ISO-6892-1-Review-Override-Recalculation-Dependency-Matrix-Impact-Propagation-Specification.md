# TB-030 — ISO 6892-1 Review/Override Recalculation Dependency Matrix & Impact Propagation Specification

**Status:** Approved / Frozen  
**Parent:** TB-029  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in

## 1. Purpose

Defines exactly which analytical Nodes and Results are affected by each Operator Override and how recalculation propagates through the dependency graph.

**Core rule:** An Override must not trigger blind full-Dataset recalculation. The system recalculates the changed Node and only the required downstream dependencies.

## 2. Dependency Graph

```text
Raw TXT
   ↓
Raw Dataset
   ↓
Normalized Dataset
   ↓
Test Boundary
   ↓
Strain Source Segmentation
   ↓
Engineering Stress / Strain
   ↓
Elastic Region
   ↓
Young's Modulus
   ↓
Yield / Rp0.2
   ↓
Rm / Necking
   ↓
Fracture
   ↓
Post-Fracture Elongation
   ↓
Horizontal Axis Correction
   ↓
Final Results
```

## 3. Impact Classes

```text
NONE
LOCAL
DOWNSTREAM
GLOBAL_ANALYSIS
```

`NONE` = no calculation impact.  
`LOCAL` = only the target Node/Result changes.  
`DOWNSTREAM` = target and dependent downstream Nodes recalculate.  
`GLOBAL_ANALYSIS` = major analytical boundary/source changes require broad recalculation.

## 4. Primary Override Impact

| Override | Impact |
|---|---|
| Test Start | GLOBAL_ANALYSIS |
| Extensometer Release | GLOBAL_ANALYSIS |
| Yield | DOWNSTREAM |
| Rp0.2 | LOCAL / validation downstream |
| Elastic Region | DOWNSTREAM |
| Rm | LOCAL / boundary validation |
| Fracture | DOWNSTREAM |
| Secondary Gauge Length | DOWNSTREAM |
| Horizontal Axis Correction | LOCAL / downstream presentation |

## 5. Main Dependency Matrix

| Override | Stress | Strain | E | Yield | Rp0.2 | Rm | Fracture | A% | Axis Correction |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Test Start | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Extensometer Release | — | ✓ | ✓ | ✓ | ✓ | — | — | ✓ | ✓ |
| Yield | — | — | conditional | ✓ | conditional | — | — | — | conditional |
| Rp0.2 | — | — | — | — | ✓ | — | — | — | — |
| Elastic Region | — | — | ✓ | ✓ | ✓ | — | — | — | ✓ |
| Rm | — | — | — | — | — | ✓ | — | — | — |
| Fracture | — | — | — | — | — | — | ✓ | ✓ | ✓ |
| Secondary Gauge Length | — | — | — | — | — | — | — | ✓ | ✓ |
| Horizontal Axis Correction | — | — | — | — | — | — | — | — | ✓ |

Conditional dependencies must follow the active ISO 6892-1 methodology configuration.

## 6. Test Start Override

Changing Test Start changes the valid Dataset boundary:

```text
TestStart
 ↓
Valid Dataset
 ↓
Strain Source
 ↓
Stress / Strain
 ↓
Elastic Region
 ↓
E
 ↓
Yield
 ↓
Rp0.2
 ↓
Rm
 ↓
Fracture
 ↓
A%
 ↓
Axis Correction
```

Impact: `GLOBAL_ANALYSIS`.

## 7. Extensometer Release Override

`ExtensometerRelease` and `Fracture` remain independent Events.

Example:

```text
Automatic Release = 840
Operator Release  = 862
```

Resulting source segmentation:

```text
0 → 862       Extensometer
862 → End     Crosshead
```

Affected calculation path:

```text
Release
 ↓
Strain Source Segmentation
 ↓
Engineering Strain
 ↓
Elastic Region
 ↓
Young's Modulus
 ↓
Yield / Rp0.2
```

Changing Release does **not** automatically move Fracture.

## 8. Yield Override

Yield is an analytical Marker/Boundary. Raw Stress and Strain arrays remain unchanged.

Depending on active Methodology, affected downstream Nodes may include Rp0.2 and Graph Correction validation.

## 9. Rp0.2 Override

Rp0.2 is recalculated locally when its search/boundary selection changes.

```text
Rp0.2 Boundary / Search
 ↓
Rp0.2
 ↓
Rp0.2 Validation
```

It does not require complete Stress–Strain Dataset reconstruction.

## 10. Elastic Region Override

Changing `ElasticStartIndex` or `ElasticEndIndex` affects:

```text
ElasticRegion
 ↓
Young's Modulus
 ↓
Yield / Rp0.2 when methodology-dependent
 ↓
Horizontal Axis Correction
```

Impact: `DOWNSTREAM`.

## 11. Young's Modulus Source

Two cases are distinguished:

### Dataset-derived E

```text
Elastic Region
 ↓
Young's Modulus
 ↓
Correction
```

### Material Library E

```text
Material Library E
 ↓
Horizontal Axis Correction
```

Changing Material Library E does not alter Raw Dataset.

## 12. Rm Override

Rm is an independent maximum/boundary Result.

Changing Rm triggers Rm recalculation/validation but does not automatically move Fracture.

```text
Rm ≠ Fracture
```

## 13. Fracture Override

Changing Fracture affects the post-fracture boundary:

```text
Fracture
 ↓
Post-Fracture Boundary
 ↓
Elongation After Fracture
 ↓
Horizontal Axis Correction
 ↓
Final A%
```

Rm is not automatically recalculated unless an explicit validation/methodology rule requires it.

## 14. Secondary Gauge Length Override

Changing `L_after` affects:

```text
L_after
 ↓
A%
 ↓
Horizontal Axis Correction
```

It does not directly affect Stress, Young's Modulus, Yield, Rp0.2 or Rm.

## 15. Horizontal Axis Correction Override

Graph correction is a downstream layer:

```text
Final Engineering Strain
 ↓
Graph Correction
 ↓
Corrected X Axis
```

It must not modify Raw Strain, Engineering Stress, Force, Displacement or source data.

## 16. Dependency Levels

Every dependency is classified as:

```text
DIRECT
INDIRECT
VALIDATION_ONLY
```

Example:

```text
ExtensometerRelease
 ↓ DIRECT
Strain
 ↓ DIRECT
YoungModulus
 ↓ INDIRECT
Rp0.2
```

## 17. Recalculation Rule

The system starts from the first changed Node rather than rereading or reimporting the TXT file.

```text
Override Applied
 ↓
Update Event / Analysis Layer
 ↓
Mark affected Node DIRTY
 ↓
Traverse Dependency Graph
 ↓
Mark downstream Nodes DIRTY
 ↓
Topological Recalculation
 ↓
Validation
```

## 18. Dirty State

Each analytical Node supports:

```text
CLEAN
DIRTY
CALCULATING
VALID
INVALID
BLOCKED
```

Example:

```text
ExtensometerRelease = VALID
Strain = DIRTY
YoungModulus = DIRTY
Rp0.2 = DIRTY
Rm = CLEAN
Fracture = CLEAN
```

## 19. Topological Calculation Order

The deterministic order is:

```text
Test Boundary
 ↓
Strain Source
 ↓
Stress / Strain
 ↓
Elastic Region
 ↓
Young's Modulus
 ↓
Yield
 ↓
Rp0.2
 ↓
Rm
 ↓
Fracture
 ↓
Post-Fracture
 ↓
Elongation
 ↓
Graph Correction
 ↓
Final Results
```

## 20. Validation Propagation

Calculation dependency and Validation dependency are distinct.

A Result can remain calculation-`CLEAN` while its validation must rerun.

Example:

```text
Fracture changed
 ↓
No Rm recalculation
 ↓
Validate: RmIndex < FractureIndex
```

Therefore:

> Clean Calculation status does not imply that Validation may be skipped.

## 21. Blocking Impact

Each Override records whether it can block Final Release:

```text
CanBlockRelease = TRUE / FALSE
```

Examples of potentially blocking states:

```text
Invalid Fracture
Invalid Rp0.2
Invalid Elastic Region
Invalid Boundary
```

## 22. Impact Object

For every Override:

```text
OverrideID
SourceNode
ImpactLevel
AffectedNodes[]
ValidationRules[]
CanBlockRelease
```

## 23. Batch Recalculation

When multiple Overrides occur in one Review Session, their downstream impact sets are unioned:

```text
Impact(Override1)
 ∪ Impact(Override2)
 ∪ Impact(Override3)
```

Only the resulting unique affected Nodes are recalculated.

## 24. No Double Calculation

Example:

```text
Release → A%
Fracture → A%
L_after → A%
```

A% is calculated once per Calculation Batch, not once per Override.

## 25. CalculationRun

Each Batch receives a unique `CalculationRunID` and records:

```text
CalculationRunID
Source Overrides
Affected Nodes
StartTimestamp
EndTimestamp
Status
```

## 26. Failure Handling

If a Node calculation fails:

```text
Node = INVALID
```

and affected downstream Nodes become:

```text
BLOCKED
```

Example:

```text
Invalid Extensometer Release
 ↓
Strain = INVALID
 ↓
YoungModulus = BLOCKED
 ↓
Rp0.2 = BLOCKED
```

## 27. Recovery

After correcting the source Override:

```text
New Override
 ↓
Rebuild Impact Set
 ↓
Recalculate affected path
 ↓
Validate
```

Only the required path is rerun.

## 28. Provenance

Every Result must be traceable through:

```text
Result
 ↓
CalculationRun
 ↓
Override(s), where applicable
 ↓
ReviewSession
 ↓
PackageVersion
 ↓
Source TXT
```

## 29. Detailed MVP Matrix

| Source Node | Direct Recalc | Downstream Recalc | Validation |
|---|---|---|---|
| TestStart | Dataset Boundary | Full analysis | Full |
| ExtensometerRelease | Strain Source | E, Yield, Rp0.2, A%, Correction | Related |
| Yield | Yield | Rp0.2 if methodology-dependent | Related |
| Rp0.2 | Rp0.2 | None | Rp0.2 |
| ElasticRegion | E | Yield/Rp0.2/Correction | Related |
| Rm | Rm | None | Rm/Boundary |
| Fracture | Fracture Boundary | A%/Correction | Boundary |
| L_after | Measurement | A%/Correction | A% |
| AxisCorrection | Corrected Axis | Final Presentation | Graph |

## 30. Independent Event Rule

The following Events remain independent:

```text
ExtensometerRelease
Yield
Rm
Fracture
```

Changing one does not silently change another. Any propagation between independent Events requires an explicit approved methodology/validation rule.

## 31. Scope Exclusions

TB-030 does not define:

- PLC
- Machine Control
- Real-Time Acquisition
- TXT modification
- LIMS
- Cloud
- Detailed UI design

The specification is limited to Review/Override impact propagation and recalculation for exported TXT-file analysis.

## 32. Freeze Decisions

| ID | Decision |
|---|---|
| D-628 | Every Override has a defined Source Node. |
| D-629 | Dependency propagates only from Upstream to Downstream. |
| D-630 | Raw Dataset is never marked dirty by an Override. |
| D-631 | Every analytical Node has Dirty/Clean/Valid/Invalid/Blocked states. |
| D-632 | Recalculation is Topological and Deterministic. |
| D-633 | ExtensometerRelease and Fracture remain independent Events. |
| D-634 | Rm correction does not automatically change Fracture. |
| D-635 | Fracture correction does not automatically change Rm. |
| D-636 | Secondary Gauge Length directly affects A% and dependent Correction only. |
| D-637 | Horizontal Axis Correction never modifies Raw Strain. |
| D-638 | Validation Dependency may trigger without Calculation Rebuild. |
| D-639 | Multiple Overrides are combined into one Impact Union per Batch. |
| D-640 | Each Node is calculated at most once per Calculation Batch. |
| D-641 | A failed Node blocks its affected downstream Nodes. |
| D-642 | Each Calculation Batch has an independent CalculationRunID. |
| D-643 | Result provenance is traceable back to Source TXT. |
| D-644 | An Override Impact may block Final Release. |
| D-645 | Recalculation runs only affected Nodes. |
| D-646 | All rules apply only to exported TXT-file analysis. |

**Status: Approved / Frozen — TB-030.**
