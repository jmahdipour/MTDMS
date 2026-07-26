# Math Core Architecture

Document ID : MTDMS-CAL-001

Version : 1.0

Status

Core Engine

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Primary Dataset

EngineeringDataset

Application

MTDMS

---

# Purpose

Math Core is the mathematical foundation of MTDMS.

Every engineering calculation inside the software shall be performed using this library.

No engineering algorithm shall directly manipulate worksheet cells.

---

# Architecture

EngineeringDataset

↓

Math Core

↓

Engineering Calculation Engine

↓

Graph Engine

↓

Report Engine

---

# Design Principles

The Math Core shall be

• Array Based

• Vector Oriented

• Independent from Excel

• Independent from SQLite

• Independent from TXT

• Reusable

---

# Responsibilities

Vector Operations

Interpolation

Differentiation

Integration

Filtering

Smoothing

Searching

Statistics

Regression

Linear Algebra

---

# Forbidden

The Math Core shall never

Read TXT

Read Worksheet

Write Worksheet

Read SQLite

Generate Reports

Draw Graphs

It only performs mathematics.

---

# Data Model

Input

```
Double()

Long()

Boolean()

```

Output

```
Double()

Long()

Boolean()

```

Objects are never modified unless explicitly requested.

---

# Array Standard

Every function receives arrays.

Example

```vb
Stress()

Strain()

Force()

Crosshead()
```

No Worksheet references allowed.

---

# Memory Model

```
Input Array

↓

Temporary Buffer

↓

Output Array

```

Temporary buffers are automatically released.

---

# Numerical Precision

Internal Precision

Double

IEEE-754

All calculations use Double precision.

---

# Error Policy

Invalid Input

↓

Return Error Code

↓

Never Crash

Division by Zero

↓

Handled

NaN

↓

Rejected

Infinity

↓

Rejected

---

# Function Groups

Vector Mathematics

Interpolation

Regression

Statistics

Signal Processing

Geometry

Filtering

Searching

Sorting

Unit Conversion

---

# Naming Convention

Functions

```
Math_

Vec_

Stat_

Interp_

Filter_

Signal_
```

Examples

```
Math_Max()

Math_Min()

Math_Mean()

Vec_Add()

Vec_Subtract()

Interp_Linear()

Filter_MovingAverage()
```

---

# Thread Safety

Current

Single Thread

Future

Parallel Processing Ready

---

# Engineering Independence

The Math Core

contains

NO

Stress Formula

Yield Formula

Young Modulus Formula

These belong to Engineering Calculation Engine.

---

# Performance

Vector Addition

O(n)

Maximum

O(n)

Interpolation

O(n)

Search

O(n)

Sorting

O(n log n)

---

# Acceptance Criteria

✔ Array Based

✔ Double Precision

✔ Excel Independent

✔ SQLite Independent

✔ Reusable

✔ High Performance

✔ Modular

✔ ISO 17025 Compatible

---

End Of Document
