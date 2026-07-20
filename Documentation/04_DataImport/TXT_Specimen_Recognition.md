# Specimen Recognition Specification

Document ID : MTDMS-IMP-024

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

---

# Purpose

This document defines how MTDMS automatically recognizes specimen geometry after importing a TXT file.

Correct specimen recognition is mandatory because all engineering calculations depend on the specimen geometry.

Area calculations, stress calculations, strain calculations and report templates are selected from the detected specimen type.

---

# Recognition Pipeline

TXT

↓

Header

↓

Geometry Detection

↓

Dimension Validation

↓

Area Calculation

↓

Engineering Engine

---

# Recognition Priority

1

Project Settings

↓

2

Header Information

↓

3

Dimension Fields

↓

4

Operator Confirmation

---

# Supported Specimen Types

Round

Flat

Pipe

Spring

Ring

Compression Block

Custom

Future

---

# Round Specimen

Required Dimensions

Diameter

or

d

Accepted Header Names

Diameter

Dia

d

Ø

Outside Diameter

Internal Geometry

Round

Area Formula

A = πd²/4

---

# Flat Specimen

Required Dimensions

Width

Thickness

Accepted Header Names

Width

b

Thickness

t

Internal Geometry

Flat

Area Formula

A = b × t

---

# Pipe Specimen

Required Dimensions

Outside Diameter

Wall Thickness

Accepted Header Names

OD

Outside Diameter

Do

Thickness

Wall

Internal Geometry

Pipe

Area Formula

A = π(D²-(D-2t)²)/4

---

# Spring Specimen

Required Parameters

Wire Diameter

Coil Diameter

Free Length

Spring Constant

Internal Geometry

Spring

Area

Not Required

---

# Ring Stiffness Specimen

Required Parameters

Pipe Diameter

Wall Thickness

Length

Internal Geometry

Ring

Area

Calculated only when required.

---

# Compression Specimen

Required Parameters

Width

Length

Height

or

Diameter

Height

Area

Automatically calculated.

---

# Custom Specimen

If geometry cannot be determined

↓

Operator manually selects geometry.

↓

Geometry stored with project.

---

# Geometry Detection Rules

Round

Only Diameter available

↓

Round

Flat

Width and Thickness available

↓

Flat

Pipe

Outside Diameter and Thickness available

↓

Pipe

---

# Dimension Validation

Diameter

>

0

Width

>

0

Thickness

>

0

Gauge Length

>

0

Failure

↓

Engineering Validation Error

---

# Automatic Area Calculation

Area imported from TXT

↓

Compared with calculated value

Difference

≤1%

Accepted

Difference

>1%

Warning

Operator confirmation required.

---

# Geometry Storage

SQLite

tblSpecimen

Stores

Specimen ID

Geometry

Dimensions

Calculated Area

Original Area

Operator Override

Timestamp

---

# Ribbon Behaviour

After geometry detection

Relevant controls become active.

Example

Pipe

↓

Enable Ring Stiffness

↓

Disable Flat Reduction of Area

---

# Future Geometry

Tube

Profile

Wire

Foil

Composite Coupon

Reserved

---

# Acceptance Criteria

✔ Automatic geometry recognition

✔ Automatic area calculation

✔ Dimension validation

✔ SQLite storage

✔ Operator override

✔ Complete audit trail

---

End of Document
