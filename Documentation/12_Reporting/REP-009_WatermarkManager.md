# Watermark Manager

Document ID : MTDMS-REP-009

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

The Watermark Manager controls all watermark elements applied to engineering reports, certificates and exported PDF documents.

Its purpose is to clearly indicate the document status without affecting engineering information.

The module manages presentation only.

It never modifies engineering calculations.

---

# Objectives

The module shall

• Manage report watermarks

• Reflect report status

• Support configurable watermark styles

• Support multilingual watermark text

• Preserve report readability

---

# Supported Watermarks

Draft

Approved

Released

Copy

Controlled Copy

Uncontrolled Copy

Confidential

Internal Use

Obsolete

Void

Administrator configurable.

---

# Watermark Workflow

```
Report Status

↓

Watermark Manager

↓

Template

↓

Report Engine

↓

PDF

↓

Print
```

---

# Watermark Sources

Report Status

Approval Status

Release Status

Laboratory Policy

Administrator Override

---

# Watermark Placement

Supported

Center

Diagonal

Header

Footer

Background

Custom

Administrator configurable.

---

# Watermark Appearance

Properties

Text

Font

Font Size

Color

Opacity

Rotation

Position

---

# Opacity

Recommended

10 %

to

25 %

Maximum

40 %

The watermark shall never reduce readability of engineering values or graphs.

---

# Language Support

Supported

Persian

English

Arabic

Other configured languages

Example

Draft

↓

پیش‌نویس

↓

Brouillon

---

# Watermark Rules

| Report Status | Watermark |
|---------------|-----------|
| Draft | Draft |
| Under Review | Draft |
| Approved | Approved |
| Released | None (default) |
| Controlled Copy | Controlled Copy |
| Uncontrolled Copy | Uncontrolled Copy |
| Archived | Optional |
| Obsolete | Obsolete |

Administrator may customize these mappings.

---

# Engineering Protection

The watermark shall never cover

Engineering Results

Graphs

Acceptance Decision

Certificate Number

QR Code

Barcode

---

# PDF Compatibility

Watermarks shall appear in

Excel Preview

Printed Reports

Generated PDF

Watermark appearance shall remain consistent across all output formats.

---

# Watermark Validation

Verify

Correct Status

Correct Language

Correct Position

Opacity

Visibility

---

# SQLite Database

Tables

```
tblWatermark

tblWatermarkConfiguration

tblWatermarkHistory
```

---

# Audit Trail

Every watermark change records

Watermark ID

Status

Language

User

Timestamp

Reason

Computer Name

---

# Permissions

Administrator

Create

Modify

Delete

Quality Manager

Approve

Reviewer

View

Operator

Automatic Use Only

---

# Error Handling

Missing Watermark

↓

Continue

Invalid Configuration

↓

Default Watermark

Unsupported Language

↓

Fallback Language

Corrupted Configuration

↓

Reload Defaults

---

# Future Enhancements

Image Watermarks

Digital Watermarks

Security Watermarks

Invisible Watermarks

Dynamic Watermarks

Reserved

---

# Acceptance Criteria

✔ Report status clearly indicated

✔ Engineering data unobstructed

✔ Multilingual support

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete watermark history

---

End of Document
