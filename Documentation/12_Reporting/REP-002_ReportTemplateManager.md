# Report Template Manager

Document ID : MTDMS-REP-002

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

The Report Template Manager controls every report template used by MTDMS.

Its purpose is to separate engineering calculations from report appearance.

Changing a report template shall never affect engineering calculations.

Changing a report template shall never modify stored engineering data.

---

# Objectives

The Template Manager shall

• Manage report templates

• Support multiple report layouts

• Support customer-specific templates

• Support laboratory templates

• Support multilingual templates

• Support template versioning

---

# Architecture

```
Engineering Results

↓

Template Manager

↓

Template Loader

↓

Template Validator

↓

Report Engine
```

---

# Supported Templates

Universal Laboratory Report

Customer Report

Tensile Report

Compression Report

Bending Report

Spring Report

Ring Stiffness Report

Hardness Report

Impact Report

Chemical Analysis Report

Calibration Report

Custom Report

---

# Template Components

Header

Footer

Company Information

Laboratory Information

Tables

Graphs

Approval Block

Signature Area

QR Code Area

Barcode Area

Watermark

Revision Block

---

# Header Area

Contains

Laboratory Logo

Laboratory Name

Certificate Number

Revision

Customer

Project

Date

Operator

---

# Body Area

Contains

Sample Information

Engineering Results

Tables

Graphs

Acceptance Summary

Remarks

---

# Footer Area

Contains

Software Version

Report Revision

Archive ID

Generated Date

Generated Time

Page Number

---

# Dynamic Fields

Supported

Certificate Number

Sample ID

Material

Standard

Operator

Date

Revision

Customer

Project

PASS / FAIL

Measured Values

Units

Graph

QR Code

Barcode

---

# Template Types

Standard

Customer

Internal

Draft

Archived

---

# Template Storage

SQLite

and

Excel Template Folder

Supported.

Template files

shall never contain engineering data.

---

# Template Version

Each template stores

Template ID

Template Name

Version

Revision

Author

Creation Date

Last Modified

Status

---

# Template Validation

Verify

Header Exists

Footer Exists

Mandatory Fields

Table Positions

Graph Placeholders

Margins

Orientation

Paper Size

---

# Paper Sizes

Supported

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

# Language Support

Templates may exist in

Persian

English

Arabic

Other languages

Each language uses an independent template.

---

# Template Selection

Selection based on

Test Type

Customer

Standard

Language

Laboratory Policy

Administrator configurable.

---

# Missing Field Handling

If template references

Unknown Field

↓

Display Warning

↓

Leave Field Blank

↓

Continue

---

# Template Locking

Approved templates

become

Read Only

Modifications require

New Template Revision

---

# SQLite Database

Tables

```
tblTemplate

tblTemplateVersion

tblTemplateLanguage

tblTemplateHistory
```

---

# Audit Trail

Every template modification records

Template ID

Version

Revision

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

Read

Operator

Use Only

---

# Error Handling

Missing Template

↓

Abort Report

Corrupted Template

↓

Abort

Unknown Placeholder

↓

Warning

Template Version Mismatch

↓

Warning

---

# Future Enhancements

Visual Template Designer

Drag-and-Drop Layout Editor

Template Marketplace

Automatic Customer Branding

Reserved

---

# Acceptance Criteria

✔ Template independent from engineering calculations

✔ Multiple templates supported

✔ Version control supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
