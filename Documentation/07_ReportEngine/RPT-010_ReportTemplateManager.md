# Report Template Manager

Document ID : MTDMS-RPT-010

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

This document defines the Report Template Manager used by MTDMS.

The Template Manager controls the structure, appearance and content of all laboratory reports without changing the engineering calculation modules.

It allows laboratories to customize report layouts while maintaining ISO/IEC 17025 compliance.

---

# Reference Standards

ISO/IEC 17025

ISO 9001

ISO 6892-1

ASTM Standards

---

# Objectives

The Template Manager shall

• Separate report layout from calculations

• Support multiple templates

• Support multilingual reports

• Support customer-specific templates

• Support laboratory branding

• Preserve engineering integrity

---

# Architecture

```
Engineering Results

↓

Template Manager

↓

Template Loader

↓

Report Generator

↓

Preview

↓

PDF

↓

Print
```

---

# Template Types

Default Laboratory Template

Customer Template

Project Template

Standard Template

Internal Template

Calibration Template

Custom Template

---

# Template Components

Header

Footer

Logo

Laboratory Information

Customer Information

Tables

Graphs

Remarks

Approval Block

Revision Block

Barcode / QR Code (optional)

---

# Template File Structure

Each template defines

Page Layout

Margins

Fonts

Colors

Sections

Visibility Rules

Field Bindings

Graph Placement

---

# Supported Sections

Laboratory Header

Customer Information

Material Information

Specimen Information

Machine Information

Environmental Conditions

Engineering Results

Graphs

Acceptance Evaluation

Remarks

Approval

Footer

---

# Dynamic Fields

Templates shall support dynamic fields

Example

```
{CustomerName}

{CertificateNumber}

{Material}

{YieldStrength}

{UTS}

{YoungModulus}

{Date}

{Operator}
```

The Report Generator replaces these placeholders with approved engineering values.

---

# Conditional Sections

A section may be shown only if

Data Exists

Example

```
Heat Treatment

display only

if available.
```

Similarly

Graphs

Remarks

Photos

Calibration Data

may be hidden automatically.

---

# Graph Position

Templates define

Graph Width

Graph Height

Graph Position

Margins

Caption

Border

without modifying the graph itself.

---

# Company Branding

Each template may specify

Company Logo

Accreditation Logo

Header Color

Footer Color

Font

Paper Size

---

# Language Support

Templates may exist in

Persian

English

Bilingual

Future

Arabic

Reserved

All text labels are template-controlled.

---

# Page Layout

Supported

A4 Portrait

A4 Landscape

Letter

Legal

Custom

Administrator configurable.

---

# Version Control

Each template has

Template ID

Version

Revision

Author

Creation Date

Last Modification

Approval Status

---

# Template Database

SQLite

Table

```
tblReportTemplate
```

Fields

TemplateID

TemplateName

Version

Revision

Language

ReportType

Author

Approved

Default

---

# Template Selection

Selection Priority

Customer Template

↓

Project Template

↓

Laboratory Default

If no custom template exists

the laboratory default template is used.

---

# Security

Approved templates

are read-only.

Editing an approved template creates

a new revision.

Old revisions remain archived.

---

# Preview

The Template Manager shall support

Live Preview

before report generation.

Engineering values remain unchanged.

---

# Error Handling

Missing Template

↓

Load Default

Invalid Placeholder

↓

Ignore

Missing Dynamic Field

↓

Display Blank

Corrupted Template

↓

Abort

---

# Future Enhancements

HTML Templates

XML Templates

JSON Templates

Customer Logo Library

Automatic Template Download

Theme Manager

Reserved

---

# Acceptance Criteria

✔ Independent from calculations

✔ Supports multiple templates

✔ Dynamic placeholders

✔ Conditional sections

✔ Multilingual

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Revision controlled

---

End of Document
