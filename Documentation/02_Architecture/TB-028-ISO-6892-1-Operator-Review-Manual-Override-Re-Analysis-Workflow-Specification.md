# TB-028 — ISO 6892-1 Operator Review, Manual Override & Re-Analysis Workflow Specification

**Status:** Approved / Frozen  
**Parent:** TB-027  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in

## 1. Purpose

Defines the Operator Review workflow for analytical Results whose automatic detection requires confirmation or correction.

The Operator never edits the Raw TXT or RawDataset. The Operator may override an Event, Boundary, Parameter, Measurement or Graph Correction. Affected dependencies are recalculated and revalidated.

## 2. Reviewable Items

```text
TestStart
ExtensometerRelease
Yield
Rp0.2
ElasticRegion
Rm
Fracture
SecondaryGaugeLength
HorizontalAxisCorrection
```

## 3. Main Workflow

```text
Automatic Analysis
 ↓
Validation
 ↓
Review Required?
 ├─ No  → Accepted
 └─ Yes → Operator Review
             ↓
       Accept / Override
             ↓
         Recalculate
             ↓
          Validate
             ↓
           Accept
             ↓
          Finalize
```

## 4. Source Immutability

The following are never editable by Operator Review:

```text
Original TXT
RawDataset
OriginalRowIndex
Original Force
Original Displacement
Original Time
```

## 5. Override Record

Every override contains:

```text
OverrideID
ObjectType
ObjectID
AutomaticValue
OperatorValue
FinalValue
Operator
Timestamp
Reason
Status
```

## 6. Override Types

```text
EVENT_OVERRIDE
BOUNDARY_OVERRIDE
PARAMETER_OVERRIDE
GRAPH_CORRECTION
MEASUREMENT_OVERRIDE
```

## 7. Event Override

For applicable Events such as ExtensometerRelease, Yield, Rp0.2, Rm and Fracture, the Operator may change the analytical index.

Example:

```text
Automatic Fracture Index = 1532
Operator Fracture Index  = 1541
```

The Raw Dataset remains unchanged.

## 8. Extensometer Release Override

`ExtensometerRelease` remains an independent Event.

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

All affected Results are recalculated.

## 9. Yield Override

Operator may correct the Yield Marker through the approved Graph Review mechanism.

The package retains:

```text
AutomaticYieldIndex
OperatorYieldIndex
FinalYieldIndex
```

Stress and Strain Raw/Normalized arrays are not modified.

## 10. Rp0.2 Override

Operator may review or correct the approved Rp0.2 search region or resulting Event where the automatic analysis is ambiguous.

After correction:

```text
Rp0.2
 ↓
Validation
```

must be executed again.

## 11. Elastic Region Override

Operator may define or correct:

```text
ElasticStartIndex
ElasticEndIndex
```

where the approved methodology permits manual review.

Affected Young's Modulus and Graph Correction Results are recalculated.

## 12. Rm Override

Rm must remain within the approved valid stress Dataset and necking/Rm boundary rules.

Workflow:

```text
Automatic Rm
 ↓
Operator Review
 ↓
Final Rm
```

## 13. Fracture Override

Fracture is an independent Event.

Changing it affects the post-fracture boundary and any dependent elongation Result.

```text
Fracture
 ↓
Post-Fracture Boundary
 ↓
A%
```

## 14. Secondary Gauge Length

Operator may enter or correct the measured post-fracture secondary gauge length:

```text
L_after
```

The value, unit, provenance and audit record are retained.

Affected Results are recalculated.

## 15. Horizontal Axis Correction

Where enabled, Graph Correction may depend on:

```text
YoungModulus
ElasticRegion
L0
L_after
```

Correction is represented by parameters and does not modify Raw Strain.

## 16. Review Graph

During Review, the Graph may display temporary verification objects:

```text
Yield Marker
Rp0.2 Line
Elastic Fit
Rm Marker
Fracture Marker
Extensometer Release Marker
Correction Line
```

These are Review-layer objects.

## 17. Review Graph vs Final Report

Review visualization and Final Report visualization are separate layers.

Temporary markers, guides and Operator verification objects must not automatically appear in the Final Report.

## 18. Automatic Acceptance

Operator may accept an automatic detection without changing it:

```text
Automatic Value
 ↓
Operator Accept
 ↓
Final Value = Automatic Value
```

The acceptance action is audited.

## 19. Override Requires Recalculation

Entering an Override does not make it a Final Result.

Required sequence:

```text
Override
 ↓
Recalculate
 ↓
Validate
 ↓
Operator Accept
 ↓
Final
```

## 20. Dependency Recalculation

### ExtensometerRelease

```text
ExtensometerRelease
 ↓
Strain Source
 ↓
Strain
 ↓
YoungModulus
 ↓
Rp0.2
```

Additional dependent Results are recalculated according to the Result Dependency Graph.

### Fracture

```text
Fracture
 ↓
Valid Dataset Boundary
 ↓
Post-Fracture Region
 ↓
A%
```

### Secondary Gauge Length

```text
L_after
 ↓
A%
 ↓
Horizontal Axis Correction
```

## 21. Re-Analysis

Re-analysis never modifies the previous Finalized Package Version.

```text
Package V1 FINALIZED
        ↓
Create Analysis V2
        ↓
Apply Override
        ↓
Recalculate
        ↓
Validate
        ↓
Review
        ↓
Finalize V2
```

## 22. Re-Analysis Reason

Every Re-analysis requires:

```text
ReasonCode
ReasonText
```

Approved examples:

```text
EVENT_CORRECTION
FRACTURE_CORRECTION
EXTENSOMETER_BOUNDARY_CORRECTION
GAUGE_LENGTH_CORRECTION
GRAPH_CORRECTION
OPERATOR_REVIEW
```

## 23. Version Relationship

New versions record:

```text
ParentPackageID
ParentPackageVersion
NewPackageVersion
ReanalysisReason
```

## 24. Audit Example

```text
Object: ExtensometerRelease
Automatic: 840
Operator: 862
Reason: Automatic transition detected late
Operator: recorded Operator ID
Timestamp: recorded Timestamp
```

## 25. Multiple Overrides

Multiple corrections may be performed in one Review Session:

```text
ExtensometerRelease
Fracture
L_after
```

MVP may batch the resulting recalculation:

```text
Review Session
 ↓
Multiple Overrides
 ↓
Single Recalculation
 ↓
Validation
 ↓
Acceptance
```

## 26. Cancel Review

Cancelling an open Review Session discards unsaved overrides and leaves the source Package Version unchanged.

## 27. Undo

Undo applies only to unsaved changes in the current Review Session.

After Finalization, correction is performed by creating a new Package Version rather than editing the finalized version.

## 28. Review Session

Each Review Session contains:

```text
ReviewSessionID
PackageVersion
Operator
StartTime
EndTime
Status
```

Status:

```text
OPEN
COMPLETED
CANCELLED
```

## 29. Review Completion

A Review Session may be completed only after:

```text
All Overrides Valid
 ↓
Recalculate
 ↓
Validate
 ↓
No Blocking Error
 ↓
Review Completed
```

## 30. Confidence

Automatic detections may carry:

```text
HIGH
MEDIUM
LOW
```

Low confidence may trigger `REVIEW_REQUIRED`, but Confidence does not itself replace Acceptance.

## 31. Automatic vs Operator Decision

The system retains:

```text
Automatic Decision
Operator Decision
Final Decision
```

Example:

```text
Automatic = Index 1532
Operator  = Index 1541
Final     = Index 1541
```

## 32. Method Immutability During Review

Operator Review cannot silently change ISO 6892-1 to another Method within the same Package Version.

Method changes require a new Analysis Version / Configuration Snapshot.

## 33. Raw Data Protection

The following operations are prohibited:

```text
Force[index] = NewValue
Strain[index] = NewValue
Time[index] = NewValue
Displacement[index] = NewValue
```

Corrections must be represented as Events, Boundaries, Parameters, Measurements or Correction objects.

## 34. Graph Correction Representation

Graph Correction is stored as:

```text
CorrectionType
Reference
Parameters
OriginalResult
CorrectedResult
```

and remains traceable to the underlying Dataset.

## 35. Acceptance After Correction

Every correction affecting a released Result requires:

```text
Correction
 ↓
Recalculate
 ↓
Validate
 ↓
Accept
```

before Finalization.

## 36. Invalid Override

If an Operator enters an invalid value:

```text
Override = INVALID
Review Session = OPEN
Release = BLOCKED
```

The previous valid Package Version remains unchanged.

## 37. Complete Example

```text
TXT
 ↓
Automatic Analysis
 ↓
Fracture = 1532
ExtensometerRelease = 840
L_after = 64.8
 ↓
REVIEW_REQUIRED
 ↓
Operator Review
 ↓
Fracture → 1541
ExtensometerRelease → 862
L_after → 65.4
 ↓
RECALCULATE
 ↓
Strain
YoungModulus
Rp0.2
A%
Horizontal Axis
 ↓
VALIDATE
 ↓
ACCEPT
 ↓
FINALIZE V2
```

## 38. MVP Requirements

The MVP must support:

- Event acceptance.
- Event override.
- Extensometer Release correction.
- Yield correction.
- Fracture correction.
- Secondary Gauge Length entry/correction.
- Graph Correction acceptance.
- Recalculation.
- Re-validation.
- Correction reason capture.
- Versioned Re-analysis.

## 39. Scope Exclusions

TB-028 excludes:

- PLC
- Machine control
- Real-time acquisition
- Editing the original TXT
- LIMS
- Cloud services
- Multi-user editing
- Electronic-signature infrastructure

All workflow rules apply exclusively to exported TXT-file analysis.

## 40. Freeze Decisions

| ID | Decision |
|---|---|
| D-584 | Operator only overrides the Analysis Layer. |
| D-585 | Raw TXT and RawDataset are immutable. |
| D-586 | Automatic and Operator values are both retained. |
| D-587 | Override without Audit is prohibited. |
| D-588 | Override requires Recalculation and Validation before Finalization. |
| D-589 | ExtensometerRelease and Fracture are independent Events. |
| D-590 | Yield and Rp0.2 overrides do not modify Raw Dataset. |
| D-591 | Secondary Gauge Length is a traceable Analysis Measurement/Input. |
| D-592 | Horizontal Axis Correction does not modify Raw Strain. |
| D-593 | Review Graph and Final Report Graph are separate layers. |
| D-594 | Review markers must not automatically appear in the Final Report. |
| D-595 | Multiple Overrides may be performed in one Review Session. |
| D-596 | MVP may batch recalculation at the end of a Review Session. |
| D-597 | Re-analysis creates a new Package Version. |
| D-598 | Finalized Package Versions are not edited in place. |
| D-599 | Re-analysis reason is mandatory. |
| D-600 | Method change requires a new Analysis Version. |
| D-601 | Operator cannot modify Raw Force/Time/Displacement/Strain arrays. |
| D-602 | Review Session has its own identifier and lifecycle status. |
| D-603 | Confidence can trigger Review but does not replace Acceptance. |
| D-604 | All workflow rules apply only to exported TXT-file analysis. |

**Status: Approved / Frozen — TB-028.**
