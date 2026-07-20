# FATEK PLC Machine Profile

Document ID : MTDMS-IMP-018

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Machine Type

FATEK PLC Based Universal Testing Machine

---

# Purpose

This document defines the standard Machine Profile for all testing machines controlled by a FATEK PLC.

Unlike Shimadzu, the PLC does not define the engineering format.

The engineering format is defined by MTDMS.

The PLC only supplies raw measured values.

---

# Supported PLC

FATEK FB Series

FATEK B1

FATEK B1z

FATEK FBS

Future Models

Compatible

---

# Communication

TXT Export

Supported

Future

Ethernet

Modbus TCP

OPC

Reserved

---

# Data Source

PLC

↓

Controller Software

↓

TXT Export

↓

MTDMS Import

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

Machine Header

↓

Internal Header

Machine

↓

MachineName

Operator

↓

Operator

Material

↓

Material

Specimen

↓

SpecimenID

Area

↓

Area

L0

↓

GaugeLength

Standard

↓

Standard

Date

↓

TestDate

Time

↓

TestTime

---

# Data Mapping

PLC Output

↓

Internal Column

Time

↓

Time

Force

↓

Force

Stroke

↓

Stroke

Extension

↓

Extension

Channel1

↓

Reserved

Channel2

↓

Reserved

Temperature

↓

Temperature

---

# Force Units

Supported

N

kN

kgf

Internal

Newton

---

# Stroke Units

Supported

mm

Internal

mm

---

# Time Units

Supported

Second

Millisecond

Internal

Second

---

# Load Cell Configuration

Supported

Multiple Load Cells

Current Configuration

100 kg

500 kg

2 ton

10 ton

25 ton

Selected automatically according to test configuration.

---

# Extensometer Configuration

Supported

10 mm

50 mm

100 mm

Automatic selection by project settings.

---

# Machine Configuration

Stored

Machine Name

PLC Model

PLC Firmware

Load Cell

Extensometer

Operator

Project

---

# Engineering Initialization

Raw Force

↓

Engineering Stress

Raw Extension

↓

Engineering Strain

Material

↓

Young's Modulus

Standard

↓

Calculation Method

---

# Validation

Mandatory

Time

Force

Stroke

Material

Area

Gauge Length

Standard

---

# Automatic Material Lookup

Material

↓

Material Library

↓

Engineering Properties

Loaded Automatically

---

# Automatic Standard Lookup

Standard

↓

Standard Library

↓

Calculation Rules

Loaded Automatically

---

# Sampling Frequency

Typical

10 Hz

20 Hz

50 Hz

100 Hz

Future

1000 Hz

---

# Noise Handling

No filtering during import.

Filtering belongs to

Graph Engine

---

# SQLite Information Stored

Project

Machine

PLC

Load Cell

Extensometer

TXT Name

Import Date

Import Duration

Checksum

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

Communication information (future)

PLC-1001

Reserved

---

# Future Expansion

Live Ethernet Import

Automatic PLC Detection

Automatic Load Cell Identification

Automatic Extensometer Detection

Reserved

---

# Acceptance Criteria

✔ Compatible with Excel 2019

✔ Compatible with VBA

✔ Compatible with SQLite

✔ TXT Only

✔ Independent of Engineering Engine

✔ Supports Multiple Load Cells

✔ Supports Multiple Extensometers

✔ Supports All Planned Mechanical Tests

---

End of Document
