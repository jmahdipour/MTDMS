# Engineering CSV Export Engine

Document ID : MTDMS-CE-018

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Primary Data Source

TXT File

Application

MTDMS

Status

Production

---

# Purpose

The Engineering CSV Export Engine exports validated engineering results and engineering graph data into standardized CSV files.

The exported CSV files are intended for long-term archiving, data exchange, statistical analysis, and compatibility with external engineering software.

The export process never modifies engineering data.

---

# Objectives

The CSV Export Engine shall

• Export engineering results

• Export engineering curves

• Preserve engineering precision

• Support standardized formats

• Support ISO-compatible exports

---

# Engineering Philosophy

TXT File

↓

Engineering Calculation

↓

Validation

↓

CSV Export

CSV files are generated

only

from validated engineering results.

---

# Export Sources

Engineering Results

Engineering Dataset

Graph Dataset

Validation Results

Material Information

Machine Information

Operator Information

Report Metadata

---

# Workflow

```
Engineering Results

↓

Validation

↓

Select Export Profile

↓

Generate CSV

↓

Save File

↓

Audit Trail
```

---

# Supported Export Types

Engineering Results

Stress–Strain Curve

True Stress–Strain Curve

Force–Displacement Curve

Spring Force–Displacement

Ring Stiffness Curve

Compression Curve

Bending Curve

Administrator configurable.

---

# CSV Encoding

Supported

UTF-8

UTF-8 with BOM

ANSI

Administrator configurable.

---

# Delimiter

Supported

Comma

Semicolon

Tab

Administrator configurable.

---

# Decimal Separator

Supported

.

,

Administrator configurable.

---

# Engineering Precision

Exported values

shall retain

full engineering precision.

Formatting inside Excel

shall never reduce exported precision.

---

# Header Information

The export may include

Report Number

Certificate Number

Material

Customer

Machine

Operator

Date

Time

Standard

Software Version

Configuration Profile

Administrator configurable.

---

# Data Columns

Typical export

Time

Force

Displacement

Extension

Engineering Stress

Engineering Strain

True Stress

True Strain

Validation Flags

---

# File Naming

Recommended

```
ReportNumber_YYYYMMDD_HHMM.csv
```

Administrator configurable.

---

# Engineering Independence

CSV export

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Only copies are exported.

---

# SQLite Interaction

SQLite stores

Export History

Export Profile

Export Timestamp

Operator

Destination Folder

CSV files themselves are not stored in SQLite.

---

# Error Handling

Invalid Folder

↓

Abort

Disk Full

↓

Abort

Permission Denied

↓

Abort

Missing Dataset

↓

Abort

Validation Failed

↓

Abort

---

# Performance Targets

Engineering Results Export

< 200 ms

Typical Tensile Curve Export

< 500 ms

Large Dataset

< 2 s

---

# Acceptance Criteria

✔ Engineering results exported

✔ Engineering curves exported

✔ Full precision preserved

✔ Multiple delimiters supported

✔ UTF-8 supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete reproducibility from TXT

---

End of Document
