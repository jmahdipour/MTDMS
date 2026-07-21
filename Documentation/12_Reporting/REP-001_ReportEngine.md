# Report Engine

Document ID : MTDMS-REP-001

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

The Report Engine is responsible for generating every engineering report produced by MTDMS.

It converts validated engineering data into standardized laboratory reports.

The Report Engine

does not perform engineering calculations.

It only formats, organizes and presents validated data.

---

# Objectives

The Report Engine shall

• Generate engineering reports

• Generate test certificates

• Generate laboratory summaries

• Support multiple templates

• Support multilingual reports

• Produce printable reports

• Produce PDF reports

---

# Report Workflow

Engineering Engine

↓

Validated Results

↓

Template Manager

↓

Report Engine

↓

Preview

↓

Approval

↓

PDF

↓

Archive

---

# Report Architecture

```
Engineering Results

↓

Template

↓

Report Builder

↓

Graph Engine

↓

Table Engine

↓

Header

↓

Footer

↓

Preview

↓

Print

↓

PDF
```

---

# Report Sources

Engineering Dataset

Material Library

Standard Library

Laboratory Information

Customer Information

Graphs

Acceptance Decision

Approval Information

Archive Information

---

# Supported Report Types

Tensile Test

Compression Test

Bending Test

Spring Test

Ring Stiffness

Rockwell Hardness

Brinell Hardness

Vickers Hardness

Charpy Impact

Chemical Analysis

Custom Report

Administrator configurable.

---

# Report Components

Header

↓

Customer Information

↓

Sample Information

↓

Material Information

↓

Engineering Results

↓

Graphs

↓

Acceptance Summary

↓

Remarks

↓

Approval

↓

Footer

---

# Header

Contains

Laboratory Name

Logo

Certificate Number

Revision

Date

Customer

Project

Operator

---

# Sample Information

Contains

Sample ID

Material

Heat Number

Dimensions

Cross Section

Gauge Length

Specimen Type

Standard

---

# Engineering Results

Displays

Validated Engineering Results

Only

No calculations performed inside the report.

---

# Graph Section

Supported

Stress-Strain

Force-Displacement

Force-Extension

Bending Curve

Spring Curve

Ring Stiffness Curve

Future Graph Types

Graphs are inserted from the validated graph engine.

---

# Acceptance Section

Displays

PASS

FAIL

NOT EVALUATED

Reference Standard

Reviewer

Approval Date

---

# Footer

Contains

Software Version

Report Revision

Page Number

Archive ID

Generated Date

Generated Time

---

# Report Status

Draft

Reviewed

Approved

Released

Archived

---

# Page Layout

Default

A4

Portrait

Landscape

Administrator configurable.

---

# Margins

Top

Bottom

Left

Right

Administrator configurable.

---

# Report Preview

Supported

Zoom

Fit Width

Fit Page

Page Navigation

Print Preview

---

# Export

Supported

Excel

PDF

Printer

Archive Package

---

# SQLite Database

Tables

```
tblReport

tblReportType

tblReportHistory

tblReportStatus
```

---

# Audit Trail

Every report generation records

Report ID

Certificate Number

Revision

Operator

Timestamp

Template

Report Type

Software Version

---

# Permissions

Administrator

Full Access

Reviewer

Generate

Operator

Generate Draft

Guest

No Access

---

# Error Handling

Missing Template

↓

Abort

Missing Graph

↓

Warning

Missing Engineering Result

↓

Abort

Printer Unavailable

↓

Warning

PDF Failure

↓

Abort

---

# Future Enhancements

Interactive Reports

Embedded Hyperlinks

Digital Signature Integration

Automatic E-mail Distribution

Cloud Report Publishing

Reserved

---

# Acceptance Criteria

✔ Engineering independent

✔ Multiple report types

✔ Printable

✔ PDF compatible

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
