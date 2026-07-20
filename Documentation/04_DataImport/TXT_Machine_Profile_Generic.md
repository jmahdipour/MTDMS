# Generic Machine Profile

Document ID : MTDMS-IMP-019

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Profile

Generic Universal Machine

---

# Purpose

This profile allows MTDMS to import TXT files from unknown or unsupported testing machines.

If no specific Machine Profile exists, this profile shall be used.

The Engineering Engine shall continue to operate normally.

---

# Philosophy

Unknown Machine

↓

Generic Profile

↓

Universal Mapping

↓

Engineering Engine

No engineering module shall know which machine generated the TXT.

---

# Supported Machines

Unknown Universal Testing Machines

Legacy Machines

Laboratory Custom Machines

Educational Machines

Research Machines

Future Machines

---

# Required Header

Minimum Required

Machine

Material

Area

Gauge Length

Standard

Force Unit

Length Unit

Date

---

# Required Columns

Time

Force

Stroke

---

# Optional Columns

Extension

Stress

Strain

Temperature

Humidity

Speed

Channel

Cycle

Reserved Columns

Ignored

---

# Automatic Column Recognition

Recognized Aliases

Force

Load

Testing Force

Applied Force

↓

Force

Stroke

Travel

Displacement

Crosshead

↓

Stroke

Time

Elapsed

Seconds

Test Time

↓

Time

Extension

Elongation

Gauge Extension

Extensometer

↓

Extension

---

# Supported Units

Force

N

kN

kgf

tf

Length

mm

cm

m

inch

Stress

MPa

N/mm²

psi

ksi

Time

Second

Millisecond

Minute

Temperature

°C

°F

Kelvin

---

# Automatic Conversion

Every value converted into

Force

Newton

Length

Millimeter

Stress

MPa

Time

Second

Temperature

°C

---

# Geometry Recognition

Supported

Round

Flat

Pipe

Spring

Ring

Unknown Geometry

↓

Operator Confirmation

---

# Material Recognition

Material

↓

Material Library

↓

Found

↓

Engineering Properties Loaded

↓

Continue

Not Found

↓

Operator Warning

↓

Continue

---

# Standard Recognition

Supported

ISO

ASTM

INSO

DIN

EN

Unknown

↓

Warning

↓

Continue

---

# Validation Rules

Mandatory

Time

Force

Stroke

Area

Gauge Length

Material

Standard

---

# Missing Columns

Extension

↓

Calculated

Stress

↓

Calculated

Strain

↓

Calculated

---

# Unsupported Data

Ignored

Binary

Images

Comments

Reserved Columns

Unknown Channels

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

# Database Storage

Machine Profile

Generic

Profile Version

Stored

Original Header

Stored

Original Units

Stored

Converted Units

Stored

---

# Logging

Import Log

Machine Unknown

Profile Used

Generic

Operator Confirmation

Stored

---

# Future Upgrade

If a dedicated profile becomes available

↓

Old projects remain compatible

↓

No database migration required

---

# Acceptance Criteria

✔ Imports unknown TXT formats

✔ Uses universal mapping

✔ Compatible with Engineering Engine

✔ Compatible with Graph Engine

✔ Compatible with Report Engine

✔ No code modification required

✔ Excel 2019 compatible

✔ VBA compatible

---

End of Document
