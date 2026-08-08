# TB-005 — Strain Source Segmentation & Event Engine

**Document:** TB-005  
**Project:** MTDMS — Material Test Data Management System  
**Version:** 1.0  
**Status:** Approved / Frozen  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in  
**Calculation model:** Array-Based

---

## 1. Purpose

TB-005 defines the logic for strain-source segmentation and management of the principal test Events.

The approved architecture treats the following as independent:

```text
YieldPoint
ExtensometerReleasePoint
FracturePoint
```

The architecture also supports explicit strain-source switching:

```text
CROSSHEAD
EXTENSOMETER
```

The raw TXT data is never modified by source switching.

---

## 2. Strain Sources

Two raw columns can provide strain information:

```text
EXTENSOMETER → Deformationt()
CROSSHEAD    → Displacement()
```

The Event Engine chooses which source is active at each Dataset index.

---

## 3. Initial Strain Source

The approved initial source is:

```text
CROSSHEAD
```

The operator may manually switch the active source to the extensometer at a selected Dataset index.

---

## 4. Source State Machine

```text
CROSSHEAD
    │
    │ Manual Extensometer Switch
    ▼
EXTENSOMETER
    │
    │ Extensometer Release Event
    ▼
CROSSHEAD
```

The state machine is an analysis representation only. It does not control laboratory hardware.

---

## 5. Independent Events

The principal Events are:

```text
YieldPoint
ExtensometerStartPoint
ExtensometerReleasePoint
FracturePoint
```

`YieldPoint`, `ExtensometerReleasePoint`, and `FracturePoint` are independent.

The system must never assume:

```text
YieldPoint = ExtensometerReleasePoint
```

or:

```text
FracturePoint = UTSPoint
```

without an explicitly approved method.

---

## 6. Yield Point

The Yield Event contains at least:

```text
Index
Time
Force
Stress
Strain
Method
OperatorConfirmed
```

Supported method classifications:

```text
AUTO
MANUAL
LIBRARY_ASSISTED
```

The Yield Event is an engineering-analysis result, not an extensometer hardware event.

---

## 7. Extensometer Start Point

When the operator manually switches the strain source to the extensometer, the selected Dataset index is stored as:

```text
ExtensometerStartPoint.Index
```

This creates the first Extensometer segment boundary.

The operation does not modify `Deformationt()` or `Displacement()`.

---

## 8. Extensometer Release Point

When the extensometer is released from the specimen, the selected Dataset index is stored as:

```text
ExtensometerReleasePoint.Index
```

From the release boundary onward, the approved strain source returns to Crosshead.

The release Event is independently recorded with provenance and confirmation status.

---

## 9. Fracture Point

Fracture is an independent Event containing at least:

```text
Index
Time
Displacement
Force
Stress
Strain
DetectionMethod
OperatorConfirmed
```

Fracture detection/confirmation must not be inferred merely from Yield or Extensometer Release.

---

## 10. StrainSource Array

Every valid Dataset point receives a source classification:

```text
StrainSource(i)
```

Allowed values:

```text
CROSSHEAD
EXTENSOMETER
```

Example:

```text
1 ... 500       → CROSSHEAD
501 ... 2200    → EXTENSOMETER
2201 ... 4200   → CROSSHEAD
```

---

## 11. Segment Structure

Each strain segment conceptually contains:

```text
StrainSegment
├── SegmentID
├── Source
├── StartIndex
├── EndIndex
├── StartEvent
├── EndEvent
└── Status
```

Example:

```text
Segment 1
Source = CROSSHEAD
Start = 1
End = 500

Segment 2
Source = EXTENSOMETER
Start = 501
End = 2200

Segment 3
Source = CROSSHEAD
Start = 2201
End = FractureIndex
```

---

## 12. Master Index

All Events are referenced by the Dataset master index.

The primary reference is:

```text
DatasetIndex
```

not Time or Displacement.

Therefore an Event always identifies an exact Dataset point.

---

## 13. Example Event Mapping

Example:

```text
YieldPoint.Index              = 1800
ExtensometerReleasePoint.Index = 2200
FracturePoint.Index            = 4500
```

The Event Engine uses these indexes to build the applicable strain-source segments.

---

## 14. Event Ordering Validation

The Event Engine validates that all Event indexes are inside the Dataset range:

```text
1 <= EventIndex <= PointCount
```

Events outside the Dataset are invalid.

The system also reports unusual ordering instead of silently correcting it.

For example:

```text
FractureIndex < ExtensometerReleaseIndex
```

is an abnormal condition that requires validation/confirmation.

---

## 15. Yield Can Occur Before or After Release

The architecture deliberately supports both cases.

### Case A

```text
Yield = 1800
Release = 2200
```

Yield occurs while the extensometer source is active.

### Case B

```text
Release = 2200
Yield = 2500
```

Yield occurs after the source has returned to Crosshead.

Both cases are structurally valid; engineering validation determines whether the resulting test interpretation is acceptable.

---

## 16. Manual Event Editing

Graph Analysis permits an operator to adjust Event indexes where the approved workflow allows manual verification.

Examples:

```text
Yield: 1850 → 1872
Release: 2200 → 2215
Fracture: 4200 → 4210
```

The original and revised values must remain auditable.

---

## 17. Event History

Manual Event changes are recorded conceptually as:

```text
EventHistory
├── EventType
├── OldIndex
├── NewIndex
├── Method
├── Operator
├── Timestamp
└── Reason
```

This is required for traceability of operator corrections.

---

## 18. Strain Assembly

After Event and segment boundaries are established, the calculation pipeline assembles:

```text
CrossheadStrain()
ExtensometerStrain()
StrainSource()
```

into:

```text
EngineeringStrain()
```

Conceptually:

```text
For each Dataset point:

    if Source = CROSSHEAD
        EngineeringStrain = CrossheadStrain

    if Source = EXTENSOMETER
        EngineeringStrain = ExtensometerStrain
```

The actual implementation remains array-based and does not read Worksheet cells point-by-point.

---

## 19. Raw Data Preservation

Source switching must never change:

```text
Displacement()
Deformationt()
Force()
Time()
No()
```

The distinction is:

```text
Source Selection ≠ Raw Data Modification
```

---

## 20. Material Library Assistance

Material Library may assist Yield analysis by defining an expected candidate region.

Conceptual flow:

```text
Material Library
       ↓
Expected Yield Region
       ↓
Candidate Window
       ↓
Automatic / Manual Analysis
       ↓
YieldPoint
```

Library values are reference/guidance data and do not automatically replace measured results.

---

## 21. Graph Correction Re-analysis

Graph Correction may cause the Event Analysis workflow to be revisited:

```text
TXT
 ↓
Dataset
 ↓
Initial Events
 ↓
Graph Analysis
 ↓
Material Library
 ↓
Operator Correction
 ↓
Final Events
 ↓
Corrected Graph
```

Events are therefore part of Analysis State, not part of the raw TXT file.

---

## 22. Secondary Length

`SecondaryLength` is not an Event.

It is a measured analysis input:

```text
SecondaryLength
├── Value
├── Unit
├── Operator
├── Timestamp
└── MeasurementMethod
```

It is used later by Graph Correction and post-fracture elongation calculations.

---

## 23. Fracture vs Secondary Length

These are independent concepts:

```text
FracturePoint
```

identifies the Dataset point associated with fracture.

```text
SecondaryLength
```

is the operator-measured post-test gauge length.

Therefore:

```text
FracturePoint ≠ SecondaryLength
```

---

## 24. Graph Correction Relationship

The Event Engine supplies Graph Correction with:

```text
YieldPoint
ExtensometerStartPoint
ExtensometerReleasePoint
FracturePoint
StrainSegments()
StrainSource()
```

Graph Correction can then use the approved Material Library and Secondary Length inputs without modifying raw source arrays.

---

## 25. Analysis State Machine

The overall analysis state is conceptually:

```text
IMPORTED
   ↓
ANALYZING
   ↓
EVENTS_IDENTIFIED
   ↓
OPERATOR_VERIFIED
   ↓
CALCULATED
   ↓
GRAPH_CORRECTED
   ↓
REPORT_READY
```

These are analysis states only; they do not represent machine-control states.

---

## 26. Example Complete Test

Example Dataset event mapping:

```text
Point 1–450
    Source = CROSSHEAD

Point 451
    ExtensometerStartPoint

Point 451–1850
    Source = EXTENSOMETER

Point 1600
    YieldPoint

Point 1850
    ExtensometerReleasePoint

Point 1851–4200
    Source = CROSSHEAD

Point 4200
    FracturePoint
```

Resulting segments:

```text
Segment 1:
CROSSHEAD
1 → 450

Segment 2:
EXTENSOMETER
451 → 1850

Segment 3:
CROSSHEAD
1851 → 4200
```

Events remain independently addressable:

```text
Yield = 1600
Release = 1850
Fracture = 4200
```

---

## 27. Automatic Detection Scope

TB-005 intentionally does **not** freeze the detailed automatic algorithms for:

- Yield detection;
- Extensometer release detection;
- Fracture detection.

Those algorithms must be defined separately against the applicable test standard and validated before implementation.

Until then, manual/operator-confirmed Event selection remains an explicitly supported analysis path.

---

## 28. Approved Design Decisions

| ID | Decision |
|---|---|
| D-48 | Initial strain source is Crosshead. |
| D-49 | Operator can manually switch the source to Extensometer. |
| D-50 | Extensometer Release is an independent Event. |
| D-51 | After Extensometer Release, the strain source returns to Crosshead. |
| D-52 | YieldPoint is independent from Extensometer Release. |
| D-53 | FracturePoint is independent from Yield and Release. |
| D-54 | Events are stored using Dataset Index as the primary point reference. |
| D-55 | Raw Displacement and Deformationt arrays are never modified by source switching. |
| D-56 | Strain segments are constructed from Event/source boundary indexes. |
| D-57 | Material Library can assist Yield candidate-region analysis. |
| D-58 | SecondaryLength is a measurement input, not an Event. |
| D-59 | Event History records manual Event changes. |
| D-60 | EngineeringStrain is assembled from the active source for each point. |
| D-61 | Detailed automatic Event-detection algorithms remain deferred until separately standardized and validated. |

---

## 29. Next Blueprint

**TB-006 — Yield Detection, Fracture Detection & Graph Analysis Methodology**

The next document will define the engineering methods for identifying Yield, Fracture, elastic-region analysis, Material Library candidate windows, operator verification, and the boundary between calculated results and graph-correction analysis.

No application code is defined by this document.
