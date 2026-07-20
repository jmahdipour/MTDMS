# TXT Graph Correction Preparation

Document ID : MTDMS-IMP-031

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Database

SQLite

---

# Purpose

This document defines how graph correction data is prepared before the operator performs any graphical correction.

Graph correction never modifies Raw Data.

Graph correction never modifies Engineering Data.

Only the display coordinates used for visualization are corrected.

---

# Philosophy

Raw Data

↓

Engineering Data

↓

Graph Dataset

↓

Graph Correction Layer

↓

Displayed Graph

---

# Data Layers

Layer 1

Raw Data

Read Only

Layer 2

Engineering Data

Calculated

Layer 3

Display Data

Corrected

Temporary

Layer 4

Report Graph

Generated

---

# Correction Workflow

Engineering Data

↓

Elastic Region

↓

Young's Modulus

↓

Reference Line

↓

Horizontal Correction

↓

Corrected Display Dataset

---

# Objective

Align the elastic region of the displayed graph with the Young's Modulus stored in the Material Library.

This correction affects visualization only.

---

# Correction Source

Required Inputs

Material

↓

Young's Modulus

Area

Gauge Length

Engineering Stress

Engineering Strain

---

# Display Correction

Correction applies only to

X Coordinates

Examples

Engineering Strain

Extension

Stroke

Y Coordinates remain unchanged.

---

# Reference Values

Young's Modulus

Loaded from

Material Library

↓

Elastic Slope

↓

Reference Line

---

# Elastic Region

Engineering Engine determines

Elastic Start

Elastic End

Graph Correction begins only inside this region.

---

# Reference Line

Reference Line

Starts

Origin

Ends

Elastic Region End

Slope

Young's Modulus

---

# Horizontal Shift

Correction calculates

Required horizontal displacement

for every point inside the elastic region.

---

# Beyond Yield

Points after Yield

Remain unchanged

unless operator requests

Full Graph Correction.

---

# Manual Correction

Operator may

Move Yield Marker

↓

Reference Line updated

↓

Display recalculated

Engineering values remain unchanged.

---

# Corrected Dataset

Temporary Array

Contains

Display X

Display Y

Marker Positions

Reference Line

Yield Line

Fracture Position

---

# SQLite Storage

No corrected display coordinates stored.

Only operator settings

may be stored.

---

# Ribbon Commands

Prepare Correction

Apply Display Correction

Reset Correction

Accept Yield

Reject Yield

Recalculate

---

# Report Generation

Reports always use

Accepted Display Graph

Engineering values remain unchanged.

---

# Reset

Reset removes

Display Corrections

Original Engineering Graph restored immediately.

---

# Performance

100000 Samples

Correction Layer

Target

<1 second

---

# Future Features

Multiple Correction Profiles

Automatic Necking Alignment

Plastic Region Alignment

Adaptive Elastic Fit

Reserved

---

# Acceptance Criteria

✔ Raw Data unchanged

✔ Engineering Data unchanged

✔ Only display coordinates corrected

✔ Young's Modulus controls correction

✔ Reset restores original graph

✔ Compatible with Excel Charts

✔ ISO 6892-1 compliant visualization

---

End of Document
