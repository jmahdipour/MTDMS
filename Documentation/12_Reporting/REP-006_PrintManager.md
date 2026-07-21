# Print Manager

Document ID : MTDMS-REP-006

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

The Print Manager is responsible for producing printed laboratory reports from validated engineering data.

The module controls print preparation only.

It does not modify engineering calculations.

It does not modify report contents.

---

# Reference Standards

ISO/IEC 17025

ISO 9001

Laboratory Quality Manual

---

# Objectives

The Print Manager shall

• Prepare printable reports

• Preserve report formatting

• Preserve graph quality

• Support different printers

• Support multiple paper sizes

• Support batch printing

---

# Workflow

```
Validated Report

↓

Print Manager

↓

Printer Verification

↓

Page Layout

↓

Preview

↓

Print

↓

Print Log
```

---

# Print Sources

Excel Report

Graphs

Tables

Customer Information

Engineering Results

Approval Block

Footer

---

# Print Modes

Single Report

Batch Reports

Draft Copy

Approved Copy

Archive Copy

Administrator configurable.

---

# Supported Paper Sizes

A4

Letter

Legal

A3

Custom

Administrator configurable.

---

# Orientation

Portrait

Landscape

Automatic

Administrator configurable.

---

# Print Quality

Draft

Normal

High

Printer Default

Administrator configurable.

---

# Margins

Top

Bottom

Left

Right

Header

Footer

Administrator configurable.

---

# Print Scaling

100%

Fit Width

Fit Page

Custom Scale

Administrator configurable.

Scaling shall never distort graphs.

---

# Graph Printing

Graphs shall preserve

Aspect Ratio

Axis Labels

Markers

Legends

Resolution

Minimum recommended

300 DPI

---

# Page Numbering

Supported

Page X of Y

Certificate Number

Revision

Optional

Print Timestamp

---

# Watermark

Optional

Draft

Approved

Copy

Confidential

Administrator configurable.

---

# Print Preview

Supported

Zoom

Multiple Pages

Page Navigation

Printer Selection

---

# Printer Selection

Supported

Default Printer

User Selected Printer

Network Printer

PDF Printer

---

# Batch Printing

Supported

Date Range

Customer

Material

Test Type

Certificate Range

Archive Selection

---

# Print Verification

Verify

Printer Available

Paper Available

Print Success

Page Count

No Print Errors

---

# SQLite Database

Tables

```
tblPrintHistory

tblPrinterConfiguration

tblPrintQueue
```

---

# Audit Trail

Every print operation records

Certificate Number

Revision

Operator

Printer

Timestamp

Print Mode

Page Count

Computer Name

---

# Permissions

Administrator

Full Access

Quality Manager

Print Approved Reports

Reviewer

Print Draft

Operator

Print Draft Only

---

# Error Handling

Printer Offline

↓

Abort

Paper Missing

↓

Pause

Print Failure

↓

Retry

Report Missing

↓

Abort

---

# Future Enhancements

Secure Printing

Digital Watermark

Cloud Print

Print Queue Monitoring

Automatic Duplex

Reserved

---

# Acceptance Criteria

✔ Accurate printed reports

✔ Graph integrity preserved

✔ Batch printing supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unchanged

✔ ISO/IEC 17025 compliant

✔ Complete print history

---

End of Document
