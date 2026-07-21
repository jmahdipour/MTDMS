# PDF Generator

Document ID : MTDMS-REP-004

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

The PDF Generator converts approved engineering reports into non-editable PDF documents suitable for delivery, archiving and long-term storage.

The module exports only approved report content.

It never performs engineering calculations.

It never modifies engineering data.

---

# Reference Standards

ISO/IEC 17025

ISO 19005 (PDF/A Recommended)

ISO 15489

Laboratory Quality Manual

---

# Objectives

The PDF Generator shall

• Produce high-quality PDF reports

• Preserve report formatting

• Preserve graphs

• Preserve traceability

• Support archival storage

• Support secure distribution

---

# Workflow

```
Validated Report

↓

PDF Generator

↓

Layout Verification

↓

Font Verification

↓

Image Verification

↓

Generate PDF

↓

Integrity Verification

↓

Archive
```

---

# Input Sources

Approved Report

Graphs

Material Information

Engineering Results

Acceptance Decision

Revision Information

Certificate Information

---

# Output

Portable Document Format

PDF

One report

↓

One PDF

---

# PDF Layout

Maintain

Page Size

Margins

Header

Footer

Fonts

Tables

Images

Graphs

Page Numbering

No layout modifications are permitted during export.

---

# Supported Paper Sizes

A4

Letter

Legal

Custom

Administrator configurable.

---

# Orientation

Portrait

Landscape

Administrator configurable.

---

# Resolution

Minimum

300 DPI

Recommended

600 DPI

Graphs shall remain readable after printing.

---

# Font Handling

Embedded fonts

Recommended

Supported fonts

Configured by template.

Font substitution shall generate a warning.

---

# Image Handling

Supported

PNG

JPEG

BMP

EMF

WMF

SVG (Future)

---

# Graph Handling

Graphs shall be exported

without loss of engineering information.

Graph scaling shall preserve

Aspect Ratio

Axis Labels

Engineering Markers

Legends

---

# Metadata

Each PDF contains

Certificate Number

Revision

Generation Date

Software Version

Archive ID

Author

Title

Keywords (optional)

---

# PDF Naming

Default

```
CertificateNumber_Revision.pdf
```

Example

```
T-2026-001245_R02.pdf
```

Administrator configurable.

---

# Security

Optional

Read Only

Password Protection

Printing Allowed

Copy Disabled

Digital Signature
(Future)

Administrator configurable.

---

# PDF Verification

Verify

File Created

Readable

Correct Page Count

Correct File Size

Checksum Generated

---

# PDF/A

Future support

PDF/A-2

for long-term archiving.

Reserved.

---

# Batch PDF Generation

Supported

Customer

Date Range

Project

Material

Test Type

Archive Selection

---

# SQLite Database

Tables

```
tblPDFHistory

tblPDFConfiguration

tblPDFVerification
```

---

# Audit Trail

Store

Certificate Number

Revision

Operator

Timestamp

PDF Name

Destination

Verification Result

Computer Name

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

Missing Report

↓

Abort

Missing Graph

↓

Abort

Font Error

↓

Warning

PDF Creation Failure

↓

Abort

Verification Failure

↓

Delete PDF

↓

Retry

---

# Future Enhancements

PDF/A Support

Digital Signature

Electronic Timestamp

Encrypted Distribution

Cloud Storage

Reserved

---

# Acceptance Criteria

✔ High-quality PDF

✔ Graph integrity preserved

✔ Metadata embedded

✔ Batch generation supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unchanged

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
