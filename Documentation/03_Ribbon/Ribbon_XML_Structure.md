# Ribbon XML Structure

Document ID : MTDMS-RBN-002

Version : 0.1.0

Platform

Microsoft Excel 2019

Technology

Office Ribbon XML

Workbook

WorkbookTemplate.xlsm

---

# Purpose

This document defines the complete Ribbon XML hierarchy.

It does not contain implementation code.

It defines the structure that Ribbon.xml must follow.

---

# Ribbon Root

```
customUI

↓

ribbon

↓

tabs

↓

tab

↓

group

↓

button
```

---

# XML Hierarchy

```
Ribbon

├── Home

├── Import

├── Calculation

├── Graph

├── Report

├── Database

├── Settings

└── Help
```

---

# HOME

Groups

```
Project

Navigation

Recent

Libraries

Application
```

Buttons

```
New Project

Open

Save

Save As

Close

Import TXT

Recent Projects

Material Library

Standard Library

Settings

Help
```

---

# IMPORT

Groups

```
TXT

Validation

Utilities
```

Buttons

```
Browse TXT

Preview

Validate

Import

Reload

Clear

TXT Properties
```

---

# CALCULATION

Groups

```
Engineering

Mechanical Properties

Material

Verification
```

Buttons

```
Calculate

Recalculate

Young

Yield

UTS

Fracture

Correction

Validation

Material Database
```

---

# GRAPH

Groups

```
Navigation

View

Engineering

Export
```

Buttons

```
Zoom

Pan

Crosshair

Grid

Manual Yield

Manual Fracture

Undo

Reset

Export Image

Export Excel
```

---

# REPORT

Groups

```
Preview

Output

Certificate
```

Buttons

```
Preview

Print

PDF

Excel

Summary

Certificate
```

---

# DATABASE

Groups

```
Projects

Libraries

Maintenance
```

Buttons

```
Projects

History

Material Library

Standard Library

Backup

Restore

Compact
```

---

# SETTINGS

Groups

```
General

Engineering

Security
```

Buttons

```
Units

Theme

Language

TXT

Graph

Protection

Users
```

---

# HELP

Groups

```
Documentation

Support
```

Buttons

```
User Manual

Developer Manual

About

License

System Information
```

---

# Control IDs

Naming Convention

```
tabHome

grpProject

btnImportTXT

btnCalculate

btnGraph

btnReport

btnSettings
```

---

# Callback Naming

```
OnLoad()

OnAction()

GetVisible()

GetEnabled()

GetImage()

GetLabel()
```

---

# Image Naming

```
imgHome

imgImport

imgGraph

imgCalculate

imgPDF

imgDatabase
```

---

# Visibility Rules

Home

Always

Import

Always

Calculation

Project Loaded

Graph

Calculation Finished

Report

Calculation Finished

Database

Always

Settings

Always

Help

Always

---

# Enable Rules

Calculate

Enabled only after TXT import.

Graph

Enabled only after successful calculation.

Report

Enabled only after calculation completed.

PDF

Enabled only after report generated.

---

# Future Ribbon Tabs

```
Compression

Impact

Fatigue

Calibration

SPC

Administration
```

Reserved for future versions.

---

# XML Validation Rules

✔ Every control shall have a unique ID.

✔ Every button shall have an icon.

✔ Every button shall have a callback.

✔ No duplicate IDs.

✔ No unused callbacks.

✔ Ribbon XML shall validate against Office 2009 Custom UI schema.

---

End of Document
