# TB-014 — ISO 6892-1 Preload, Zero Point, Seating Region & Initial Dataset Handling Specification

**Document:** TB-014  
**Project:** MTDMS — Material Test Data Management System  
**Version:** 1.0  
**Status:** Approved / Frozen  
**Parent:** TB-005 through TB-013  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in  
**Calculation model:** Array-Based

## 1. Purpose

TB-014 defines handling of the initial portion of the TXT Dataset before the principal test region. This region may contain initial zero, seating, preload, machine stabilization, and slack-removal behavior.

## 2. Raw Data Preservation

All initial records remain in Raw Dataset. No row is deleted solely because it occurs at the beginning of the file.

## 3. Zero Point

Zero Point is an independent analysis concept. The system may retain:

```text
ZeroPointIndex
ZeroTime
ZeroDisplacement
ZeroForce
```

The first file row is not automatically treated as the valid test Zero Point.

## 4. Initial Region

An initial region may contain multiple records with approximately zero force/displacement or repeated timestamps. It is classified rather than physically removed.

## 5. Preload

Preload is independent of Zero Point. TB-014 does not define the first non-zero force as preload unless the applicable Method explicitly specifies that rule.

## 6. Seating Region

Seating is a separate classification and is not inferred solely from Force > 0. The applicable Method determines its detection/acceptance rules.

## 7. Row Phase

Each row may be classified as:

```text
INITIAL
SEATING
PRELOAD
TEST
POST_TEST
```

Classification is analysis state, not deletion.

## 8. Calculation Eligibility

`CalculationEligible(i)` is independent from `RowPhase(i)`. A classified initial row may remain calculation-eligible when the applicable Method requires it.

## 9. Curve Start

The engineering curve may use a `CurveStartIndex` without deleting earlier raw rows. Raw Dataset remains complete.

## 10. Zero Correction

If configured by the applicable Method, derived arrays may apply zero correction:

```text
CorrectedForce(i) = ForceN(i) - ZeroForce
CorrectedDisplacement(i) = Displacement(i) - ZeroDisplacement
ElapsedTime(i) = Time(i) - ZeroTime
```

Raw arrays are never overwritten.

## 11. No Automatic Zeroing

The system must not silently execute first-value subtraction such as:

```text
ForceCorrected = Force - FirstForce
```

without an explicit Method/Configuration rule.

## 12. Duplicate Initial Time

Rows with identical initial timestamps are retained. They may be produced by the source file structure and are not automatically treated as duplicates for deletion.

## 13. Extensometer Relationship

Initial/Seating/Preload boundaries are independent of Extensometer Attach and Release Events. The Extensometer source sequence remains governed by TB-005.

## 14. Event Independence

The following are independent events:

```text
ZeroPointEvent
PreloadEvent
TestStartEvent
ExtensometerAttachEvent
ExtensometerReleaseEvent
YieldEvent
RmEvent
FractureEvent
```

## 15. Manual Boundary Selection

Operator-selected Zero, Preload, or Test Start boundaries are recorded as Events rather than silently modifying the Dataset.

Each manual Event retains:

```text
DatasetIndex
Operator
Timestamp
Reason
Comment
```

## 16. Automatic Detection and Override

Automatic classification may be overridden manually. The original automatic result remains traceable, together with the manual override.

Each boundary may record:

```text
DetectionSource
AUTOMATIC | MANUAL | METHOD_DEFINED
```

## 17. Initial Region and Elastic Analysis

TB-014 supplies initial-state information to TB-011. TB-011 remains responsible for selecting the Elastic Region and Young's Modulus calculation range.

## 18. Initial Region and Rp0.2

TB-008 may consume `TestStartIndex` and other approved boundaries. TB-014 does not calculate Rp0.2.

## 19. Initial Region and Rm

TB-009 consumes the appropriate analysis boundaries. Initial rows are not automatically included in Rm search.

## 20. Graph View

Graph View may expose controls such as:

```text
Show Initial Region
Hide Initial Region
Show Preload
Hide Preload
```

Hiding is a View operation only.

## 21. Reporting

Initial/Preload/Seating information may be included in Test Conditions or Traceability sections when configured. Initial rows are not automatically plotted in the final report.

## 22. Raw Export

Raw export preserves the complete Raw Dataset, including all initial, seating, and preload rows.

## 23. Corrected Export

Corrected export may use calculation eligibility and correction state but must preserve lineage to the Raw Dataset.

## 24. Array Integrity

Raw parallel arrays retain identical length:

```text
Length(No)
= Length(Time)
= Length(Displacement)
= Length(Deformationt)
= Length(Force)
```

Derived arrays must not silently alter Raw Array length.

## 25. Phase Detection Pipeline

```text
Raw Arrays
   ↓
Initial Classification
   ↓
Boundary Events
   ↓
Derived Correction Arrays
   ↓
Calculation Eligibility
   ↓
Curve Dataset
```

## 26. Data Lineage

Every boundary and classification remains traceable to the original Dataset Index and TXT row.

## 27. Audit Trail

Manual changes retain at least:

```text
Operator
Timestamp
OldValue
NewValue
Reason
```

## 28. Freeze Decisions

| ID | Decision |
|---|---|
| D-231 | Raw Initial Rows are never automatically deleted. |
| D-232 | First Row is not automatically the Zero Point. |
| D-233 | Zero Point, Preload, and Test Start are independent Events. |
| D-234 | Initial/Seating/Preload are classifications, not physical deletion rules. |
| D-235 | Preload is not inferred from First Non-Zero Force without a Method rule. |
| D-236 | Duplicate initial timestamps are preserved. |
| D-237 | Initial Zero Force and Zero Displacement rows are not automatically deleted. |
| D-238 | Zero correction is implemented through derived arrays only. |
| D-239 | Raw Force and Raw Displacement are never overwritten. |
| D-240 | Extensometer Attach/Release Events are independent of Initial/Preload Events. |
| D-241 | TestStartIndex is an independent boundary. |
| D-242 | Manual Zero/Preload/TestStart selections are recorded as Events and audit records. |
| D-243 | Automatic detection may be manually overridden without destroying the original automatic result. |
| D-244 | Initial Region is not automatically used in Rp0.2/Rm/Elastic analysis. |
| D-245 | Raw Export preserves all Initial Rows. |
| D-246 | Derived arrays do not alter Raw Array length. |
| D-247 | No boundary changes silently. |
| D-248 | Calculation Eligibility is independent of RowPhase. |
| D-249 | Boundary-to-raw-row Data Lineage is mandatory. |

## 29. Status

**Approved / Frozen — TB-014.**
