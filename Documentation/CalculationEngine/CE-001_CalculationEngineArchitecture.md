# Calculation Engine Architecture

Document ID : MTDMS-CE-001

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Input

TXT File

Application

MTDMS

Status

Production

---

# Purpose

The Calculation Engine is the core engineering component of MTDMS.

It receives the machine-generated TXT file and converts raw measurement data into validated engineering results.

The Calculation Engine is independent of the report format and independent of the SQLite database.

SQLite stores only the results.

---

# Objectives

The Calculation Engine shall

• Read TXT files

• Validate imported data

• Perform engineering calculations

• Generate engineering graphs

• Produce engineering results

• Supply validated data to reporting modules

---

# Engineering Philosophy

TXT File

↓

Import

↓

Validation

↓

Engineering Calculation

↓

Engineering Results

↓

Report

↓

Certificate

The TXT file is always the engineering source.

Every calculation can be reproduced from the TXT file.

---

# General Workflow

```
TXT File

↓

TXT Parser

↓

Data Validation

↓

Unit Normalization

↓

Geometry Calculation

↓

Engineering Calculation

↓

Graph Generation

↓

Engineering Validation

↓

Engineering Results

↓

SQLite

↓

Excel Report
```

---

# Input

Machine TXT File

Examples

Shimadzu

Universal Testing Machine

Spring Tester

Ring Stiffness Tester

Other supported devices

---

# Output

Engineering Results

Engineering Graphs

Validation Results

Report Data

Certificate Data

CSV Export

---

# Calculation Modules

TXT Parsing Engine

↓

Geometry Engine

↓

Unit Conversion Engine

↓

Material Reference Engine

↓

Engineering Formula Engine

↓

Graph Engine

↓

Validation Engine

↓

Reporting Engine

Each module is independent.

---

# Supported Test Types

Tensile Test

Compression Test

Three-Point Bending

Four-Point Bending

Spring Constant

Ring Stiffness

Plastic Tensile

Future Tests

Administrator configurable.

---

# Engineering Rules

Engineering calculations

shall never

use

previous reports

previous calculations

cached results

Every calculation starts from

the imported TXT file.

---

# Geometry

Geometry calculations

may use

Diameter

Width

Thickness

Gauge Length

Secondary Gauge Length

Operator Input

Material Library

Geometry is calculated

before

engineering calculations.

---

# Material Library

The Material Library

may provide

Reference Young's Modulus

Reference Yield Strength

Reference Tensile Strength

Reference Elongation

Reference values

never replace

measured values.

---

# Unit Handling

The engine internally converts

all quantities

to

SI units.

Presentation units

are selected later

during reporting.

---

# Graph Generation

Graphs are generated

after

engineering calculations.

Graphs use

engineering values

not

raw display values.

---

# Validation

Every engineering result

shall be validated

before

report generation.

Validation uses

Standard Database

Calculation Profile

Material Library

Machine Capability

---

# Database Interaction

Calculation Engine

does not

calculate

inside SQLite.

SQLite is used only for

Storage

History

Configuration

Audit

Reports

---

# Excel Interaction

The engine writes

validated engineering values

to Excel.

Excel performs

presentation only.

Excel shall not perform

engineering calculations.

---

# Error Handling

TXT Missing

↓

Abort

TXT Corrupted

↓

Abort

Geometry Failure

↓

Reject

Calculation Failure

↓

Reject

Validation Failure

↓

Warning

---

# Performance Targets

TXT Parsing

< 200 ms

Geometry

< 50 ms

Engineering Calculation

< 500 ms

Validation

< 200 ms

Graph Generation

< 1 second

---

# Acceptance Criteria

✔ Calculation starts from TXT

✔ No dependence on previous calculations

✔ SQLite stores results only

✔ Excel displays results only

✔ Engineering reproducibility guaranteed

✔ Excel 2019 compatible

✔ SQLite compatible

✔ ISO/IEC 17025 compliant

---

End of Document
