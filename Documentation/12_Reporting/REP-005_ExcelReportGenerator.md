# Excel Report Generator

Document ID : MTDMS-REP-005

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Reporting

Status

Production

---

# Purpose

The Excel Report Generator creates the native Excel report used inside MTDMS.

This report is the master editable document from which PDF, printing and archival copies are generated.

The module formats validated engineering results only.

No engineering calculations are performed during report generation.

---

# Reference Standards

ISO/IEC 17025

ISO 9001

Laboratory Quality Manual

---

# Objectives

The Excel Report Generator shall

• Generate editable Excel reports

• Preserve engineering formatting

• Preserve graph quality

• Support templates

• Support multilingual reports

• Support future revisions

---

# Workflow

```
Validated Engineering Results

↓

Template Manager

↓

Excel Report Generator

↓

Workbook

↓

Preview

↓

Review

↓

PDF

↓

Archive
```

---

# Workbook Structure

Default

```
Workbook

│

├── Report

├── Graphs

├── Calculation Summary

├── Validation Summary

├── Metadata

└── Hidden Internal Data
```

Hidden worksheets are protected.

---

# Report Worksheet

Contains

Header

Customer Information

Material Information

Engineering Results

Graphs

Acceptance Summary

Approval Block

Footer

---

# Graph Worksheet

Contains

Validated engineering graphs

One graph per report section

Graphs remain linked to validated data only.

---

# Validation Worksheet

Contains

Validation Summary

Engineering Validation

Graph Validation

Acceptance Validation

Release Status

Normally hidden.

---

# Metadata Worksheet

Contains

Certificate Number

Revision

Archive ID

Software Version

Template Version

Generation Date

Normally hidden.

---

# Formatting

Supports

Merged Cells

Borders

Conditional Formatting

Cell Protection

Named Ranges

Page Breaks

Print Areas

---

# Supported Features

Auto Page Number

Dynamic Tables

Automatic Headers

Automatic Footers

Automatic Date

Automatic Revision

---

# Images

Supported

Laboratory Logo

Customer Logo

Graphs

QR Code

Barcode

Signature Image (Future)

---

# Worksheet Protection

Editable

Remarks

Customer Notes

Reviewer Notes

Protected

Engineering Results

Certificate Number

Revision

Graphs

Validation Data

---

# Print Areas

Configured automatically

One report

↓

One print area

Multiple-page reports supported.

---

# File Naming

Default

```
CertificateNumber_Revision.xlsx
```

Example

```
T-2026-001245_R02.xlsx
```

Administrator configurable.

---

# Export Compatibility

Native Excel

↓

PDF Generator

↓

Print Manager

↓

Archive Manager

---

# Template Compatibility

The workbook uses only

Approved Templates

Template version recorded inside metadata.

---

# SQLite Database

Tables

```
tblExcelReport

tblExcelTemplate

tblWorkbookHistory
```

---

# Audit Trail

Record

Workbook Name

Certificate Number

Revision

Template

Operator

Timestamp

Software Version

---

# Permissions

Administrator

Full Access

Quality Manager

Generate

Reviewer

Generate

Operator

Draft Only

---

# Error Handling

Missing Template

↓

Abort

Worksheet Missing

↓

Abort

Graph Missing

↓

Abort

Workbook Save Failure

↓

Retry

---

# Future Enhancements

Macro-Free Reports

Password Protected Workbook

Digital Signature

Cloud Workbook

Collaborative Review

Reserved

---

# Acceptance Criteria

✔ Native Excel workbook

✔ Editable report

✔ Protected engineering data

✔ Template based

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unchanged

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
