# Named Ranges Specification

Document ID : MTDMS-WB-004

Version : 0.1.0

Platform

Microsoft Excel 2019

Workbook

WorkbookTemplate.xlsm

---

# Purpose

This document defines every Named Range used inside WorkbookTemplate.xlsm.

Rules

• Every important cell shall have a Name.

• VBA shall never use hard-coded addresses.

Correct

```vb
Range("nrProjectName").Value
```

Wrong

```vb
Range("B5").Value
```

---

# Naming Convention

Prefix

nr

Example

nrProjectName

---

# HOME

| Name | Description |
|------|-------------|
| nrProjectName | Current Project |
| nrCustomer | Customer Name |
| nrOperator | Operator |
| nrMachine | Machine Name |
| nrMaterial | Material |
| nrStandard | Test Standard |
| nrProjectStatus | Current Status |
| nrDate | Test Date |
| nrTime | Test Time |

---

# IMPORT

| Name | Description |
|------|-------------|
| nrTXTFile | TXT File Name |
| nrTXTPath | TXT Folder |
| nrMachineType | Machine Type |
| nrTXTEncoding | Encoding |
| nrImportStatus | Import Status |
| nrValidationStatus | Validation Result |

---

# ANALYSIS

| Name | Description |
|------|-------------|
| nrArea | Cross Section Area |
| nrGaugeLength | Initial Gauge Length |
| nrDiameter | Diameter |
| nrWidth | Width |
| nrThickness | Thickness |
| nrYoung | Young's Modulus |
| nrYield | Yield Strength |
| nrUTS | Ultimate Strength |
| nrFracture | Fracture Strength |
| nrElongation | Elongation |
| nrReductionArea | Reduction of Area |

---

# GRAPH

| Name | Description |
|------|-------------|
| nrYieldPointX | Yield X |
| nrYieldPointY | Yield Y |
| nrUTSX | UTS X |
| nrUTSY | UTS Y |
| nrBreakX | Break X |
| nrBreakY | Break Y |
| nrCursorX | Cursor X |
| nrCursorY | Cursor Y |

---

# REPORT

| Name | Description |
|------|-------------|
| nrReportNumber | Report ID |
| nrApproval | Approval Status |
| nrInspector | Inspector |
| nrReviewer | Reviewer |
| nrSignature | Signature |

---

# SETTINGS

| Name | Description |
|------|-------------|
| nrLanguage | Language |
| nrUnitSystem | Unit System |
| nrTheme | UI Theme |
| nrGraphScale | Graph Scale |
| nrDatabasePath | SQLite Path |

---

# SYSTEM

| Name | Description |
|------|-------------|
| nrWorkbookVersion | Workbook Version |
| nrDatabaseVersion | Database Version |
| nrCurrentUser | Logged User |
| nrApplicationState | Current State |
| nrLastError | Last Error |

---

# Engineering Ranges

| Name | Description |
|------|-------------|
| nrStressArray | Engineering Stress Array |
| nrStrainArray | Engineering Strain Array |
| nrTrueStressArray | True Stress Array |
| nrTrueStrainArray | True Strain Array |
| nrForceArray | Force Array |
| nrStrokeArray | Stroke Array |

---

# Protection Rules

Named Ranges

Protected

Editable

Only Input Ranges

Calculation Ranges

Locked

System Ranges

Locked

---

# Design Rule

All VBA modules must access workbook data through Named Ranges.

Direct cell references are prohibited except during workbook initialization.

---

End of Document
