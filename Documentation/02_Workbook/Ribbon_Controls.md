# Ribbon Controls Specification

Document ID : MTDMS-RBN-004

Version : 0.1.0

Platform

Microsoft Excel 2019

Ribbon XML

Workbook

WorkbookTemplate.xlsm

---

# Purpose

This document defines every Ribbon control used by MTDMS.

Every control shall have

• Unique ID

• Label

• Image

• Callback

• Visibility Rule

• Enable Rule

---

# Control Types

Button

SplitButton

Menu

ToggleButton

Separator

Group

Tab

Gallery (Future)

---

# HOME TAB

## Group

Project

| ID | Label | Image | Callback |
|----|--------|--------|-----------|
| btnNewProject | New Project | imgNew | OnNewProject |
| btnOpenProject | Open Project | imgOpen | OnOpenProject |
| btnSaveProject | Save | imgSave | OnSaveProject |
| btnSaveAs | Save As | imgSaveAs | OnSaveAs |
| btnCloseProject | Close | imgClose | OnCloseProject |

---

## Group

Navigation

| ID | Label | Callback |
|----|--------|----------|
| btnHome | Home | OnHome |
| btnImport | Import | OnImport |
| btnAnalysis | Analysis | OnAnalysis |
| btnGraph | Graph | OnGraph |
| btnReport | Report | OnReport |

---

# IMPORT TAB

## Group

TXT

| ID | Label |
|----|--------|
| btnBrowseTXT | Browse TXT |
| btnPreviewTXT | Preview |
| btnValidateTXT | Validate |
| btnImportTXT | Import |
| btnReloadTXT | Reload |
| btnClearTXT | Clear |

---

# CALCULATION TAB

## Group

Engineering

| ID | Label |
|----|--------|
| btnCalculate | Calculate |
| btnRecalculate | Recalculate |
| btnCorrection | Correction |
| btnVerification | Verification |

---

## Group

Mechanical

| ID | Label |
|----|--------|
| btnYoung | Young's Modulus |
| btnYield | Yield Strength |
| btnUTS | Ultimate Strength |
| btnFracture | Fracture |
| btnTrueStress | True Stress |
| btnTrueStrain | True Strain |

---

# GRAPH TAB

## Group

View

| ID | Label |
|----|--------|
| btnZoom | Zoom |
| btnPan | Pan |
| btnCrosshair | Crosshair |
| btnGrid | Grid |

---

## Group

Engineering

| ID | Label |
|----|--------|
| btnManualYield | Manual Yield |
| btnManualFracture | Manual Fracture |
| btnUndo | Undo |
| btnReset | Reset |

---

## Group

Export

| ID | Label |
|----|--------|
| btnExportImage | Export Image |
| btnExportExcel | Export Excel |
| btnCopyGraph | Copy Graph |

---

# REPORT TAB

## Group

Output

| ID | Label |
|----|--------|
| btnPreview | Preview |
| btnPrint | Print |
| btnPDF | PDF |
| btnExcelReport | Excel |
| btnCertificate | Certificate |

---

# DATABASE TAB

## Group

Database

| ID | Label |
|----|--------|
| btnProjectDB | Projects |
| btnHistory | History |
| btnMaterialDB | Material Library |
| btnStandardDB | Standard Library |
| btnBackup | Backup |
| btnRestore | Restore |
| btnCompact | Compact |

---

# SETTINGS TAB

## Group

Application

| ID | Label |
|----|--------|
| btnGeneral | General |
| btnUnits | Units |
| btnTheme | Theme |
| btnLanguage | Language |

---

## Group

Engineering

| ID | Label |
|----|--------|
| btnGraphSettings | Graph |
| btnTXTSettings | TXT |
| btnCalculationSettings | Calculation |

---

# HELP TAB

## Group

Help

| ID | Label |
|----|--------|
| btnUserManual | User Manual |
| btnDeveloperManual | Developer Manual |
| btnAbout | About |
| btnLicense | License |
| btnSystemInfo | System Information |

---

# Visibility Rules

Always Visible

Home

Import

Settings

Help

Conditional

Calculation

Graph

Report

Database

---

# Enable Rules

Calculate

TXT Imported

TXT Valid

Project Loaded

---

Graph

Calculation Finished

---

Report

Graph Generated

---

Database

SQLite Connected

---

# Images

Every control shall contain

imageMso

or

Custom Image

No control shall appear without an icon.

---

# Localization

Labels

English

Tooltips

English

Internal IDs

English Only

---

# Reserved Controls

Compression

Impact

Fatigue

Calibration

SPC

Administrator

Cloud

Network

AI Assistant

---

End of Document
