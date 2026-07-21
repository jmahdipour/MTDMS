# PDF Export Engine

Document ID : MTDMS-RPT-009

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Report Engine

Status

Production

---

# Purpose

This document defines the PDF Export Engine used by MTDMS.

The PDF Export Engine converts approved reports into immutable PDF documents suitable for

• Customer delivery

• Regulatory submission

• ISO 17025 document control

• Long-term archival

• Electronic distribution

The generated PDF shall faithfully reproduce the approved report.

---

# Reference Standards

ISO/IEC 17025

ISO 32000-1 (PDF)

ISO 19005 (PDF/A) (Future)

---

# Design Objectives

The PDF Export Engine shall

• Produce identical output on all systems

• Preserve formatting

• Preserve engineering precision

• Embed fonts

• Preserve vector graphics

• Support digital signatures

• Prevent accidental editing

---

# Export Workflow

```
Approved Report

↓

Validation

↓

Template Rendering

↓

Graph Rendering

↓

PDF Generator

↓

Verification

↓

Archive

↓

Customer
```

---

# Export Sources

Engineering Results

Graphs

Tables

Header

Footer

Approval Block

Company Logo

QR Code (optional)

Digital Signature (optional)

---

# Supported PDF Types

Standard PDF

PDF/A (Future)

Password Protected PDF

Digitally Signed PDF (Future)

---

# Page Size

Supported

A4

Letter

Legal

Administrator configurable.

Default

A4 Portrait

---

# Orientation

Portrait

Landscape

Automatic

---

# Font Handling

All fonts

shall be embedded.

Missing fonts

shall use approved fallback fonts.

---

# Graphics

Engineering graphs

shall remain vector graphics whenever possible.

Bitmap graphics

Minimum

300 DPI

---

# Image Compression

Lossless

Preferred

Optional

JPEG High Quality

Administrator configurable.

---

# File Naming

Default

```
CertificateNo_Revision.pdf
```

Example

```
2026-00125_R01.pdf
```

---

# Metadata

Embedded PDF metadata

Title

Certificate Number

Author

Laboratory

Subject

Keywords

Creation Date

Revision

---

# Watermarks

Optional

Draft

Copy

Confidential

Approved

Rejected

Administrator configurable.

---

# Security Options

Optional

Password Protection

Print Restriction

Copy Restriction

Edit Restriction

Digital Signature

Reserved

---

# Verification

After export

verify

File Exists

Readable

Correct Page Count

Correct File Size

Embedded Fonts

Checksum

---

# PDF Quality

Text

Vector

Graphs

Vector Preferred

Tables

Native

Resolution

300 DPI

Minimum

---

# Archive

Generated PDFs

may be copied automatically to

Archive Folder

Network Storage

Customer Folder

Cloud Storage (Future)

---

# Database

SQLite

Tables

```
tblPDFExport

tblCertificate

tblExportHistory
```

Fields

Certificate Number

Revision

Export Date

Operator

File Name

Checksum

Destination

---

# Error Handling

Template Missing

↓

Abort

Graph Missing

↓

Placeholder

Disk Full

↓

Abort

Write Permission Denied

↓

Abort

Verification Failed

↓

Retry

---

# Performance Targets

Single Page Report

< 2 seconds

Large Report

< 5 seconds

Verification

< 1 second

---

# Future Enhancements

PDF/A Compliance

Electronic Signature

Embedded XML

Automatic Email

Cloud Upload

QR Verification

Reserved

---

# Acceptance Criteria

✔ ISO/IEC 17025 compliant

✔ Identical visual output

✔ Embedded fonts

✔ Vector graphs

✔ Metadata included

✔ Export verification

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Archive ready

---

End of Document
