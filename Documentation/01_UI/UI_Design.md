# User Interface Design Specification

Document ID : MTDMS-UI-001

Version : 0.1.0

Platform

Microsoft Excel 2019

Ribbon XML

VBA

---

# 1. Design Philosophy

MTDMS shall NOT look like an ordinary Excel workbook.

The user must feel they are working with an industrial software package.

Excel is only the execution platform.

The workbook is the application.

---

# 2. General Rules

✔ Ribbon Interface

✔ Full Screen

✔ No Sheet Tabs Visible

✔ No Formula Bar

✔ No Gridlines

✔ No Headings

✔ No Scrollbars (optional)

✔ No UserForms

✔ Native Excel Controls only

---

# 3. Workbook Navigation

Navigation is performed only through Ribbon.

Users shall never navigate using worksheet tabs.

Navigation Flow

HOME

↓

IMPORT

↓

ANALYSIS

↓

GRAPH

↓

REPORT

---

# 4. Screen Resolution

Reference Design

1920 × 1080

Minimum Supported

1366 × 768

Responsive Layout

YES

---

# 5. Theme

Primary Color

Dark Blue

Secondary

White

Accent

Steel Blue

Success

Green

Warning

Orange

Error

Red

Background

Light Gray

---

# 6. Typography

Font

Segoe UI

Titles

14 pt Bold

Group Titles

11 pt Bold

Normal Text

10 pt

Tables

10 pt

Status Bar

9 pt

---

# 7. Header

Every visible worksheet shall contain the same Header.

Fields

Project

Operator

Material

Standard

Machine

Specimen

Date

Status

---

# 8. Footer

Workbook Version

SQLite Status

TXT Status

Calculation Status

---

# 9. HOME Worksheet

Purpose

Dashboard

No engineering calculations are performed here.

Sections

Project

Recent Projects

Import TXT

Material Library

Settings

Help

---

# 10. IMPORT Worksheet

Purpose

TXT Import

Sections

File Selection

TXT Preview

Validation Result

Import Button

---

# 11. ANALYSIS Worksheet

Purpose

Engineering Calculations

Layout

Left Panel

Project Information

Center

Stress–Strain Graph

Right Panel

Engineering Results

Bottom

Cursor Information

---

# 12. GRAPH Worksheet

Purpose

Interactive Graph

Supported Tools

Zoom

Pan

Crosshair

Manual Yield Marker

Manual Fracture Marker

Undo

Reset

Export

---

# 13. REPORT Worksheet

Purpose

Report Preview

Buttons

Print

PDF

Excel Export

Summary

---

# 14. Hidden Worksheets

RAW_DATA

ENGINEERING

RESULT

SYSTEM

ERROR_LOG

SETTINGS

HISTORY

MATERIAL_DB

STANDARD_DB

These worksheets are never shown to ordinary users.

---

# 15. Status Colors

Ready

Green

Busy

Blue

Warning

Orange

Error

Red

---

# 16. User Interaction

Mouse

Required

Keyboard

Supported

Touch

Not Required

---

# 17. Protection

Visible worksheets

Protected

Hidden worksheets

Strongly Protected

Ribbon

Always Visible

---

# 18. UI Rules

No merged cells unless absolutely necessary.

No floating controls.

No ActiveX controls.

No UserForms.

No engineering logic inside UI sheets.

All calculations occur in ENGINEERING sheet.

UI is presentation only.

---

End of Document
