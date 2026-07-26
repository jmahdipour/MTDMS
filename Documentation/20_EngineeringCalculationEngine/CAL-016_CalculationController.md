# Calculation Controller

Document ID

MTDMS-CAL-016

Version

1.0

Status

Core Controller

Platform

Excel 2019

Language

VBA

Application

MTDMS

---

# Purpose

Calculation Controller coordinates every engineering engine.

It performs

NO

engineering calculation.

Its only responsibility is controlling execution order.

---

# Principle

Controller

↓

calls

↓

Engine

↓

stores result

↓

calls next engine

---

# Execution Order

Import

↓

Validation

↓

Preprocessing

↓

Stress Engine

↓

Strain Engine

↓

Young Engine

↓

Yield Engine

↓

Fracture Engine

↓

Graph Correction Engine

↓

Statistics Engine

↓

Graph Engine

↓

Report Engine

↓

Archive Engine

---

# Controller Responsibilities

Initialize Dataset

Run Engines

Handle Errors

Measure Execution Time

Store Audit Information

Abort when necessary

Generate Log

---

# Forbidden

Controller never

calculates stress

calculates strain

calculates modulus

calculates yield

draws graphs

writes reports

imports TXT

---

# Object Diagram

```

Calculation Controller

│

├── Validation

├── Stress

├── Strain

├── Young

├── Yield

├── Fracture

├── Graph Correction

├── Statistics

├── Graph

└── Report

```

---

# Dataset Ownership

Controller owns

EngineeringDataset

Every engine receives

By Reference

No copies.

---

# Processing Model

Dataset

↓

Stress Engine

↓

Dataset

↓

Strain Engine

↓

Dataset

↓

Young Engine

↓

Dataset

↓

Yield Engine

↓

Dataset

↓

...

---

# Error Policy

Any Critical Error

↓

Stop Pipeline

↓

Return Error

Non-Critical Error

↓

Store Warning

↓

Continue

---

# Execution State

Idle

↓

Running

↓

Completed

↓

Failed

---

# Logging

For every engine

Store

Start Time

End Time

Execution Time

Status

Warnings

Errors

---

# Audit

Controller creates

Execution History

Example

Validation

OK

12 ms

Stress

OK

4 ms

Young

OK

16 ms

Yield

Warning

8 ms

Fracture

OK

6 ms

...

---

# Performance

Only one Dataset exists.

No duplicate arrays.

No duplicate calculations.

---

# Controller Interface

Suggested Methods

Initialize()

Run()

Abort()

Reset()

GenerateLog()

---

# Acceptance

✔ Single Controller

✔ Modular

✔ Deterministic

✔ Repeatable

✔ Excel Independent

✔ ISO 17025 Compatible

---

End Of Document
