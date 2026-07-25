# Report Configuration Engine

Document ID : MTDMS-RE-025

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

The Report Configuration Engine manages all configurable parameters related to engineering reports, certificates, document generation, printing, export, localization, branding, and distribution.

Its purpose is to centralize every report-related configuration so that laboratories can adapt MTDMS without modifying program code.

The engine performs **no engineering calculations**.

---

# Objectives

The Report Configuration Engine shall

• Centralize report configuration

• Support administrator customization

• Preserve standardized reporting

• Simplify laboratory deployment

• Maintain engineering consistency

---

# Engineering Philosophy

Configuration

↓

Report Engine

↓

Engineering Report

Configuration changes behaviour only.

Engineering calculations remain unaffected.

---

# Configuration Categories

Templates

Branding

Localization

Printing

PDF

Export

Graphs

Approval

Security

Distribution

Customer Profiles

Archive

Numbering

Administrator configurable.

---

# Workflow

```
Program Start

↓

Load Configuration

↓

Apply Configuration

↓

Generate Reports
```

---

# Laboratory Configuration

Laboratory Name

Address

Telephone

Website

Email

Accreditation Number

Logo

Default Language

Administrator configurable.

---

# Report Configuration

Default Template

Page Size

Margins

Header

Footer

Summary Position

Approval Position

Administrator configurable.

---

# Graph Configuration

Default Graph

Graph Size

Graph Position

Graph Resolution

Graph Theme

Marker Visibility

Administrator configurable.

---

# Export Configuration

PDF

Excel

CSV

ZIP

Destination Folder

Administrator configurable.

---

# Approval Configuration

Approval Levels

Reviewer

Approver

Digital Signature Placeholder

Administrator configurable.

---

# Distribution Configuration

Default Destination

Automatic Distribution

Email

Archive

Network Folder

Administrator configurable.

---

# Archive Configuration

Archive Folder

Retention Policy

Compression

Backup

Administrator configurable.

---

# Numbering Configuration

Prefix

Year

Counter

Revision Format

Reset Policy

Administrator configurable.

---

# Localization Configuration

Default Language

Available Languages

Fallback Language

Dictionary Version

Administrator configurable.

---

# Customer Configuration

Preferred Language

Preferred Template

Preferred Output

Preferred Package

Preferred Distribution

Administrator configurable.

---

# Engineering Independence

The Report Configuration Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Only configuration parameters are managed.

---

# SQLite Interaction

SQLite stores

Configuration Profiles

Customer Profiles

Administrator Settings

Version History

Audit Information

---

# Error Handling

Missing Configuration

↓

Use Default

Invalid Configuration

↓

Reject

Corrupted Profile

↓

Restore Default

---

# Performance Targets

Load Configuration

< 200 ms

Apply Configuration

< 100 ms

Profile Switch

< 100 ms

---

# Acceptance Criteria

✔ Centralized configuration

✔ Administrator customization

✔ Multiple profiles

✔ Customer profiles

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
