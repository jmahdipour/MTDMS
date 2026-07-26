# Engineering Calculation Pipeline

Document ID

MTDMS-CAL-010

Version

1.0

Status

Core Engine

Platform

Excel 2019 VBA

Language

VBA

Application

MTDMS

---

# Purpose

This document defines the complete calculation workflow.

Every imported test follows exactly the same sequence.

No calculation may skip any mandatory stage.

---

# Overall Pipeline

TXT

↓

Import Engine

↓

EngineeringDataset

↓

Validation

↓

Preprocessing

↓

Engineering Calculations

↓

Graph Analysis

↓

Report

↓

Archive

---

# Stage 1

Import

Responsible

TXT Import Engine

Output

EngineeringDataset

Contains

Metadata

Raw Arrays

No calculations.

---

# Stage 2

Validation

Responsible

Validation Engine

Checks

Array Length

Metadata

Missing Values

Invalid Values

Duplicate Records

Broken Records

Output

Validated Dataset

---

# Stage 3

Preprocessing

Responsible

Preprocessing Engine

Operations

Remove Invalid Points

Remove Duplicate Time

Trim Empty Tail

Detect Extensometer

Normalize Arrays

No engineering calculations.

---

# Stage 4

Derived Arrays

Responsible

Calculation Engine

Produces

Stress()

Strain()

True Stress()

True Strain()

Engineering arrays only.

---

# Stage 5

Elastic Region Detection

Responsible

Elastic Engine

Tasks

Detect Linear Region

Largest Linear Segment

Regression

Slope

Goodness Of Fit

Output

Elastic Zone

---

# Stage 6

Young Modulus

Responsible

Young Engine

Input

Elastic Region

Output

Young Modulus

---

# Stage 7

Graph Correction

Responsible

Graph Correction Engine

Tasks

Horizontal Shift

Elastic Alignment

Gauge Length Correction

Virtual Strain

Output

Corrected Strain

---

# Stage 8

Yield Detection

Responsible

Yield Engine

Possible Methods

Upper Yield

Lower Yield

Rp0.2

Rp0.1

Rt0.5

Rt

Administrator configurable.

---

# Stage 9

Ultimate Strength

Responsible

Maximum Engine

Output

Maximum Force

Maximum Stress

Maximum Extension

Maximum Strain

---

# Stage 10

Fracture Detection

Responsible

Fracture Engine

Detect

Break Point

Last Valid Point

Fracture Extension

Fracture Strain

---

# Stage 11

Post Processing

Responsible

Statistics Engine

Generate

Maximum

Minimum

Average

Energy

Sampling Statistics

---

# Stage 12

Graph Generation

Responsible

Graph Engine

Generate

Stress-Strain

Force-Extension

Force-Time

Crosshead-Time

Custom Graphs

---

# Stage 13

Report

Responsible

Report Engine

Produces

Test Report

Summary Report

INSO 3132

Building Code Summary

Administrator configurable.

---

# Stage 14

Archive

Responsible

SQLite Engine

Stores

Metadata

Results

Audit

History

---

# Data Flow

EngineeringDataset

↓

Validation

↓

Preprocessing

↓

Stress

↓

Strain

↓

Young

↓

Correction

↓

Yield

↓

Maximum

↓

Fracture

↓

Statistics

↓

Report

---

# Rules

Each stage

Receives

↓

EngineeringDataset

Returns

↓

EngineeringDataset

No Engine returns worksheet objects.

---

# Failure Policy

Validation Failed

↓

Abort

Calculation Failed

↓

Abort

Graph Failed

↓

Continue

Report Failed

↓

Continue

SQLite Failed

↓

Warning

---

# Debug Mode

Each stage stores

Execution Time

Input Count

Output Count

Warnings

Errors

---

# Acceptance

✔ Deterministic

✔ Repeatable

✔ Modular

✔ Excel Independent

✔ Array Based

✔ Object Oriented

✔ High Performance

✔ ISO 17025 Compatible

---

End Of Document
