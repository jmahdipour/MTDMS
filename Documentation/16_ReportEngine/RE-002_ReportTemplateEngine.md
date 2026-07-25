# Report Template Engine

Document ID : MTDMS-RE-002

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Primary Data Source

TXT File (Testing Machine Export)

Application

MTDMS

Status

Production

---

# Purpose

The Report Template Engine defines and manages all engineering report templates used by MTDMS.

Templates determine only the presentation of reports.

They never contain engineering calculations.

They never modify engineering data.

---

# Objectives

The Report Template Engine shall

• Manage report templates

• Standardize report appearance

• Support multiple report formats

• Support administrator customization

• Preserve engineering consistency

---

# Engineering Philosophy

Engineering Dataset

↓

Report Template

↓

Engineering Report

The template controls appearance only.

Engineering values always originate from the Calculation Engine.

---

# Supported Templates

Tensile Test Report

Compression Report

Spring Report

Ring Stiffness Report

Three-Point Bending

Four-Point Bending

Customer Report

Internal Laboratory Report

Calibration Report

Statistical Report

Administrator configurable.

---

# Template Structure

Header

Company Logo

Laboratory Information

Report Title

Customer Information

Material Information

Machine Information

Operator Information

Engineering Results

Engineering Graph

Summary

Approval

Footer

---

# Header

The header may contain

Laboratory Name

Address

Telephone

Website

Email

Accreditation Number

Logo

Administrator configurable.

---

# Customer Section

Customer Name

Project

Order Number

Sample Identification

Heat Number

Batch Number

Purchase Order

Optional.

---

# Material Section

Material Name

Material Grade

Standard

Specification

Heat Treatment

Dimensions

Cross Section

Optional.

---

# Machine Section

Machine Name

Machine Number

Load Cell

Extensometer

Calibration Date

Software Version

Optional.

---

# Engineering Results Section

Results shall be inserted directly from validated engineering values.

The template performs no calculations.

---

# Graph Section

Graphs are inserted from the Graph Engine.

Supported

Stress–Strain

Force–Displacement

Spring

Ring Stiffness

Compression

Bending

Comparison

Administrator configurable.

---

# Summary Section

May include

Pass / Fail

Acceptance Limits

Specification Comparison

Customer Requirements

Comments

Administrator configurable.

---

# Approval Section

Prepared By

Reviewed By

Approved By

Date

Electronic Signature (future)

Administrator configurable.

---

# Footer

Page Number

Report Number

Revision

Issue Date

Confidentiality Notice

Administrator configurable.

---

# Template Versioning

Each template stores

Template ID

Revision

Version

Approval Status

Author

Creation Date

Modification Date

---

# Administrator Customization

Administrators may

Create Template

Duplicate Template

Modify Template

Delete Template

Import Template

Export Template

Assign Default Template

---

# Engineering Independence

The Report Template Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Only presentation is defined.

---

# SQLite Interaction

SQLite stores

Template Definitions

Template Versions

Default Assignments

Administrator Changes

Audit History

Templates are loaded dynamically.

---

# Error Handling

Missing Template

↓

Use Default

Corrupted Template

↓

Reject

Missing Logo

↓

Continue

Missing Optional Field

↓

Leave Blank

---

# Performance Targets

Template Load

< 100 ms

Template Selection

< 20 ms

Template Rendering

< 300 ms

---

# Acceptance Criteria

✔ Multiple templates supported

✔ Administrator customization supported

✔ Version control supported

✔ Dynamic field mapping

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
