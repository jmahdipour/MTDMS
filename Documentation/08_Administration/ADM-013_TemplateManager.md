# Template Manager

Document ID : MTDMS-ADM-013

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Administration

Status

Production

---

# Purpose

The Template Manager manages all report, certificate, label and document templates used throughout MTDMS.

It separates presentation from engineering calculations.

Changing a template shall never modify engineering results.

---

# Objectives

The Template Manager shall

• Manage report templates

• Manage certificate templates

• Manage print layouts

• Support customer-specific templates

• Support template version control

• Preserve report consistency

---

# Template Categories

Mechanical Reports

Chemical Reports

Calibration Certificates

Hardness Reports

Impact Reports

Tensile Reports

Bending Reports

Spring Reports

Ring Stiffness Reports

Labels

Internal Forms

Custom Templates

---

# Architecture

```
Engineering Results

↓

Template Manager

↓

Template Loader

↓

Layout Engine

↓

Report Engine

↓

PDF

↓

Print
```

---

# Template Components

Header

Footer

Logo

Customer Block

Material Block

Machine Block

Results Table

Graph

Remarks

Approval Block

QR Code

Barcode

Watermark

---

# Template Metadata

Template ID

Template Name

Version

Revision

Author

Creation Date

Approval Date

Language

Paper Size

Orientation

Status

---

# Template Status

Draft

Approved

Obsolete

Archived

Under Review

---

# Layout Configuration

Page Size

Margins

Columns

Row Heights

Fonts

Colors

Borders

Alignment

Spacing

---

# Dynamic Placeholders

Supported placeholders

```
{CertificateNumber}

{CustomerName}

{Material}

{SpecimenID}

{Operator}

{Date}

{YieldStrength}

{UTS}

{YoungModulus}

{Hardness}

{ImpactEnergy}
```

The Report Engine replaces placeholders during report generation.

---

# Conditional Sections

Templates may hide sections automatically

Examples

Hide Graph

if

No Graph Available

Hide Remarks

if

Empty

Hide Heat Treatment

if

Unknown

---

# Customer Templates

Each customer may have

Default Template

Company Logo

Approval Layout

Special Footer

Special Acceptance Table

Independent Report Numbering

Optional

---

# Print Configuration

Portrait

Landscape

A4

Letter

Legal

Custom

---

# Graph Placement

Graph Position

Width

Height

Margins

Caption

Legend

Graph Scaling

All configurable

without modifying the graph itself.

---

# Logo Management

Supported

PNG

JPG

BMP

Preferred

PNG

Transparent Background

---

# Watermarks

Draft

Copy

Approved

Rejected

Confidential

Administrator configurable.

---

# Version Control

Every modification creates

New Revision

Previous revisions

remain archived.

Reports always store

Template Version

used during generation.

---

# SQLite Database

Tables

```
tblTemplate

tblTemplateRevision

tblTemplateAssignment

tblCustomerTemplate
```

---

# Import

Supported

Excel

SQLite

Future

JSON

XML

---

# Export

Template Package

SQLite

Excel

Future

JSON

XML

---

# Permissions

Administrator

Full Access

Quality Manager

Approve

Report Designer

Modify Draft

Operator

Read Only

---

# Validation Rules

Duplicate Template Name

↓

Reject

Missing Header

↓

Warning

Missing Approval Block

↓

Reject

Invalid Placeholder

↓

Warning

---

# Audit Trail

Every modification records

Template

Revision

User

Date

Time

Reason

Computer Name

---

# Error Handling

Template Missing

↓

Load Default

Corrupted Template

↓

Restore Previous Revision

Unknown Placeholder

↓

Ignore

Missing Logo

↓

Use Default Logo

---

# Future Enhancements

Visual Template Designer

Drag & Drop Layout

HTML Templates

Responsive Templates

Cloud Template Repository

Reserved

---

# Acceptance Criteria

✔ Version controlled

✔ Customer-specific templates

✔ Dynamic placeholders

✔ Conditional sections

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering independent

✔ Full audit trail

---

End of Document
