# Company Logo Manager

Document ID : MTDMS-REP-008

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

The Company Logo Manager controls all graphical identity elements used in laboratory reports.

Its responsibility is to insert and manage logos without affecting engineering content.

The module never modifies engineering data.

The module only manages graphical assets.

---

# Objectives

The module shall

• Manage laboratory logos

• Manage customer logos

• Support multiple logo versions

• Preserve print quality

• Maintain consistent report appearance

• Record logo history

---

# Logo Categories

Laboratory Logo

Customer Logo

Project Logo

Accreditation Logo

Certification Logo

Confidential Mark

Future Logo Types

---

# Architecture

```
Logo Library

↓

Logo Manager

↓

Template Manager

↓

Report Engine

↓

Generated Report
```

---

# Supported Image Formats

PNG

JPEG

BMP

EMF

WMF

SVG (Future)

---

# Recommended Format

PNG

Transparent Background

Minimum Resolution

300 DPI

Recommended Resolution

600 DPI

---

# Laboratory Logo

Only one active laboratory logo is permitted.

Changing the laboratory logo

does not affect

previously archived reports.

Archived reports retain the original logo used at generation time.

---

# Customer Logo

Customer logo is optional.

Each customer may have

Zero

or

One

default logo.

The customer logo may also be overridden for an individual report.

---

# Accreditation Logo

Supported

ISO/IEC 17025

National Accreditation Body

Other accreditation marks

Visibility controlled by laboratory policy.

---

# Logo Position

Supported Positions

Top Left

Top Center

Top Right

Footer Left

Footer Right

Custom

Administrator configurable.

---

# Logo Size

Each template defines

Width

Height

Aspect Ratio

The Logo Manager shall preserve aspect ratio during resizing.

Image stretching is not permitted.

---

# Logo Validation

Verify

File Exists

Supported Format

Readable

Resolution

Aspect Ratio

Corrupted images

↓

Rejected

---

# Report Integration

Logos may appear in

Header

Footer

Cover Page

Approval Page

Certificate

Not inside engineering graphs.

---

# Version Control

Each logo stores

Logo ID

Name

Version

Owner

Activation Date

Retirement Date

Status

---

# SQLite Database

Tables

```
tblLogo

tblLogoHistory

tblCustomerLogo

tblLogoConfiguration
```

---

# Audit Trail

Every logo modification records

Logo ID

Version

User

Timestamp

Reason

Computer Name

---

# Permissions

Administrator

Upload

Modify

Delete

Quality Manager

Approve

Reviewer

View

Operator

Use Only

---

# Error Handling

Missing Logo

↓

Use Default Logo

Corrupted Image

↓

Reject

Unsupported Format

↓

Reject

Missing Customer Logo

↓

Continue

---

# Future Enhancements

Vector Logo Support

Dark Theme Logos

Automatic Customer Branding

Cloud Logo Repository

Reserved

---

# Acceptance Criteria

✔ Multiple logo types supported

✔ Aspect ratio preserved

✔ Version history maintained

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering data unaffected

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
