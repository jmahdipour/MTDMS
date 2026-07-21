# CSV Graph Export Engine

Document ID : MTDMS-GRH-010

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Graph Engine

Status

Production

---

# Purpose

This document defines the CSV Graph Export Engine.

The module exports graph datasets into standardized CSV files for

• Engineering analysis

• External software

• Finite Element programs

• Statistical analysis

• Long-term archival

• ISO 17025 traceability

The exported dataset shall preserve engineering precision.

---

# Reference Standards

ISO 6892-1

ISO 6805-1

ISO 17025

ASTM E8 / ASTM E8M

---

# Supported Export Types

Original Dataset

Corrected Dataset

Engineering Curve

True Curve

Force Curve

Extension Curve

Time Curve

User Selected Region

---

# Export Workflow

Engineering Data

↓

Validation

↓

Select Dataset

↓

CSV Generator

↓

Write File

↓

Verification

↓

Complete

---

# CSV Encoding

UTF-8

without BOM

Preferred

Windows ANSI

Optional

Administrator configurable.

---

# Decimal Separator

Always

```
.
```

Period

Independent of Windows regional settings.

---

# Column Separator

Default

```
,
```

Optional

```
;
```

Administrator configurable.

---

# Line Ending

Windows

CRLF

---

# Supported Columns

Sample Number

Time

Force

Extension

Engineering Stress

Engineering Strain

True Stress

True Strain

Plastic Strain

Marker Flag

Reserved

---

# Default Header

```
Sample,
Time(s),
Force(N),
Extension(mm),
EngineeringStress(MPa),
EngineeringStrain,
TrueStress(MPa),
TrueStrain,
PlasticStrain,
Marker
```

---

# Marker Export

If enabled

additional marker column contains

Yield

UTS

Necking

Fracture

Manual

Blank

---

# Original Export

Contains

Imported data

only.

No correction applied.

---

# Corrected Export

Contains

Corrected X values

Original Y values

Used for

presentation

only.

---

# Engineering Export

Contains

Calculated engineering values

ready for

external analysis.

---

# Precision

Internal

Double Precision

Export

Default

8 Decimal Places

Administrator configurable.

---

# File Naming

Default

```
CertificateNo_TestType_Date.csv
```

Example

```
2026-00125_Tensile_20260719.csv
```

---

# Destination

User Selected Folder

↓

Automatic Verification

↓

Overwrite Check

↓

Write File

---

# Overwrite Policy

If file exists

Prompt User

Overwrite

Rename

Cancel

---

# Export Validation

Number of rows

must equal

engineering dataset.

Column count

must match

selected export profile.

---

# Verification

After export

software shall verify

File Exists

Row Count

Column Count

Readable

No truncation

---

# SQLite Logging

Table

```
tblExportHistory
```

Fields

ExportID

FileName

ExportType

Operator

Timestamp

Destination

Status

Checksum

---

# Error Handling

Folder Missing

↓

Abort

Write Permission Denied

↓

Abort

Disk Full

↓

Abort

Encoding Failure

↓

Abort

Verification Failure

↓

Retry

---

# Compatibility

Compatible With

Excel

MATLAB

Python

R

Origin

Minitab

Abaqus

ANSYS

LS-DYNA

Custom Software

---

# Future Enhancements

Direct JSON Export

XML Export

HDF5 Export

Automatic Cloud Upload

Digital Signature

Compressed CSV

Reserved

---

# Acceptance Criteria

✔ UTF-8 export

✔ Double precision

✔ Original and corrected datasets supported

✔ ISO compatible format

✔ SQLite logging

✔ Excel 2019 compatible

✔ External software compatible

✔ Export verification performed

---

End of Document
