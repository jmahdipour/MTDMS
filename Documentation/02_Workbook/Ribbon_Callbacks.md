# Ribbon Callback Specification

Document ID : MTDMS-RBN-003

Version : 0.1.0

Platform

Microsoft Excel 2019

Ribbon XML

Language

VBA

Workbook

WorkbookTemplate.xlsm

---

# Purpose

This document defines every Ribbon callback used by MTDMS.

Ribbon callbacks shall never contain business logic.

Callbacks only redirect execution to Controller modules.

---

# Architecture

Ribbon Button

↓

Ribbon Callback

↓

RibbonController

↓

Business Controller

↓

Calculation Module

↓

Worksheet Refresh

---

# Callback Rules

Each callback

✔ One purpose

✔ One controller

✔ No worksheet manipulation

✔ No SQL

✔ No engineering calculation

---

# Ribbon Load

Callback

```
OnRibbonLoad()
```

Purpose

Store Ribbon reference.

Controller

RibbonController

---

# Navigation Callbacks

```
OnHome()

OnImport()

OnAnalysis()

OnGraph()

OnReport()

OnDatabase()

OnSettings()

OnHelp()
```

Controller

NavigationController

---

# Project Callbacks

```
OnNewProject()

OnOpenProject()

OnSaveProject()

OnSaveAs()

OnCloseProject()
```

Controller

ProjectController

---

# TXT Callbacks

```
OnBrowseTXT()

OnPreviewTXT()

OnValidateTXT()

OnImportTXT()

OnReloadTXT()

OnClearTXT()
```

Controller

ImportController

---

# Calculation Callbacks

```
OnCalculate()

OnRecalculate()

OnCorrection()

OnVerification()
```

Controller

CalculationController

---

# Mechanical Property Callbacks

```
OnYoung()

OnYield()

OnUTS()

OnFracture()

OnTrueStress()

OnTrueStrain()
```

Controller

CalculationController

---

# Material Callbacks

```
OnMaterialLibrary()

OnSelectMaterial()

OnReloadMaterial()
```

Controller

MaterialController

---

# Graph Callbacks

```
OnZoom()

OnPan()

OnCrosshair()

OnGrid()

OnManualYield()

OnManualFracture()

OnUndo()

OnReset()
```

Controller

GraphController

---

# Export Callbacks

```
OnExportImage()

OnExportExcel()

OnCopyGraph()
```

Controller

GraphController

---

# Report Callbacks

```
OnPreview()

OnPrint()

OnExportPDF()

OnExportReportExcel()

OnCertificate()
```

Controller

ReportController

---

# Database Callbacks

```
OnOpenDatabase()

OnHistory()

OnBackup()

OnRestore()

OnCompact()
```

Controller

DatabaseController

---

# Settings Callbacks

```
OnGeneralSettings()

OnGraphSettings()

OnTXTSettings()

OnEngineeringSettings()

OnLanguage()

OnTheme()
```

Controller

SettingsController

---

# Help Callbacks

```
OnUserManual()

OnDeveloperManual()

OnAbout()

OnLicense()

OnSystemInformation()
```

Controller

HelpController

---

# Dynamic Callbacks

Used by Ribbon XML

```
GetVisible()

GetEnabled()

GetLabel()

GetImage()

GetSize()

GetPressed()
```

---

# Enable Logic

Example

Calculate Button

Enabled

Project Loaded

AND

TXT Imported

AND

TXT Valid

Otherwise

Disabled

---

# Graph Button

Enabled

Engineering Calculation Completed

Otherwise

Disabled

---

# Report Button

Enabled

Calculation Completed

Otherwise

Disabled

---

# Material Library

Enabled

Always

---

# Settings

Enabled

Always

---

# Error Handling

Every callback

Must

```
On Error GoTo ErrorHandler
```

Log Error

↓

Display Message

↓

Exit Safely

---

# Performance

Target callback execution

< 20 ms

Heavy operations

Must execute inside Controller modules.

---

# Future Callbacks

```
OnCompression()

OnImpact()

OnFatigue()

OnCalibration()

OnSPC()

OnCloud()
```

Reserved.

---

# Naming Convention

Callbacks

```
OnXXXX
```

Examples

```
OnCalculate

OnGraph

OnPreview

OnImportTXT
```

Controllers

```
ControllerXXXX
```

Examples

```
CalculationController

ImportController

ReportController
```

---

End of Document
