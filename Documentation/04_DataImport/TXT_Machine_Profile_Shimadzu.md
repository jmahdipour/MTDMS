# Shimadzu Machine Profile

Document ID : MTDMS-IMP-017

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Machine

Shimadzu Universal Testing Machine

Series

Autograph

---

# Purpose

This document defines the complete import profile for Shimadzu testing machines.

This is the reference implementation for the MTDMS Import Engine.

All future machine profiles shall follow this architecture.

---

# Supported Machines

AG-IS

AG-X

AGS-X

AGS-J

AG-25TB

Future Models

Compatible

---

# Communication

TXT Export

Only

No live communication

No OPC

No Serial

No Ethernet

The parser imports exported TXT files only.

---

# Native Software

Trapezium X

Trapezium Lite

Future

Universal Export

---

# Supported Tests

Tensile

Compression

Three Point Bend

Four Point Bend

Spring

Ring Stiffness

Future

Impact

Fatigue

---

# Header Mapping

| Shimadzu Header | Internal Header |
|-----------------|----------------|
| Machine | MachineName |
| Operator | Operator |
| Material | Material |
| Specimen | SpecimenID |
| Area | Area |
| L0 | GaugeLength |
| Standard | Standard |
| Date | TestDate |
| Time | TestTime |

---

# Column Mapping

| Shimadzu | Internal |
|----------|----------|
| Time | Time |
| Force | Force |
| Stroke | Stroke |
| Extension | Extension |
| Stress | EngineeringStress |
| Strain | EngineeringStrain |

---

# Supported Units

Force

kN

N

Length

mm

Stress

MPa

Time

Second

---

# Internal Conversion

Force

↓

Newton

Length

↓

Millimeter

Stress

↓

MPa

Time

↓

Second

---

# Data Order

Expected

Time

Stroke

Extension

Force

Stress

Strain

If different

↓

Automatic Mapping

---

# Missing Columns

Extension

↓

Use Stroke

Stress

↓

Recalculate

Strain

↓

Recalculate

---

# Engineering Initialization

After Import

Engineering Controller receives

Time

Force

Stroke

Extension

Area

Gauge Length

Material

Standard

---

# Automatic Material Lookup

Material Name

↓

Material Library

↓

Load

Young's Modulus

Yield Range

UTS Range

Poisson Ratio

Density

---

# Validation Rules

Mandatory

Force

Stroke

Time

Material

Area

L0

Standard

---

# Typical Export Size

Rows

500

↓

200000

Compatible

---

# Typical Sampling Rate

10 Hz

20 Hz

50 Hz

100 Hz

Automatic Detection

---

# Noise Filtering

No filtering performed during import.

Filtering belongs to

Graph Engine

---

# Parser Behavior

Read

↓

Validate

↓

Normalize

↓

Store

↓

Return ImportResult

---

# Unsupported Features

Binary Export

Live Data

Encrypted TXT

Multiple Test Files

---

# Error Codes

Missing Force

IMP-0302

Missing Stroke

IMP-0303

Unknown Unit

IMP-0401

Invalid Header

IMP-0201

---

# Future Extensions

Direct USB Import

Network Import

Automatic Project Creation

Reserved

---

# Acceptance Criteria

✔ Shimadzu TXT imports without modification

✔ Automatic column mapping

✔ Automatic unit conversion

✔ Automatic material lookup

✔ Compatible with Engineering Engine

✔ Compatible with Report Engine

---

End of Document
