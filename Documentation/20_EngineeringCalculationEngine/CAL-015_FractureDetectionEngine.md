# Fracture Detection Engine

Document ID

MTDMS-CAL-015

Version

1.0

Status

Critical Core Engine

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Dependencies

EngineeringDataset

Stress Engine

Strain Engine

---

# Purpose

The Fracture Detection Engine determines the exact fracture location on the tensile test curve.

All calculations after fracture shall be ignored.

This engine defines the usable engineering dataset.

---

# Engineering Principle

Fracture is not simply

Maximum Force

and it is not

Last Recorded Point.

The fracture point must be determined from the engineering behaviour of the specimen.

---

# Inputs

EngineeringDataset.Raw.Force()

EngineeringDataset.Raw.Crosshead()

EngineeringDataset.Raw.Extensometer()

EngineeringDataset.Calc.Stress()

EngineeringDataset.Calc.Strain()

---

# Outputs

Fracture Index

Fracture Force

Fracture Stress

Fracture Extension

Fracture Strain

Dataset.Flags.FractureDetected

---

# Engineering Definition

Fracture Point

=

Last physically valid specimen point.

Not

Last imported point.

---

# Dataset Behaviour

Before Fracture

↓

Valid

After Fracture

↓

Ignored

---

# Detection Strategy

The engine evaluates

Force

Stress

Crosshead

Extensometer

Slope

Data continuity

to determine the fracture position.

---

# Candidate Conditions

Possible indicators

Sudden force drop

Stress collapse

Loss of continuity

End of deformation

End of extensometer signal

Operator confirmation (optional)

No single condition is sufficient by itself.

The engine evaluates all indicators together.

---

# Rule

After the fracture index is identified

all subsequent points are marked

InvalidForEngineering

The raw data remain unchanged.

---

# Dataset Flags

PointStatus()

Valid

Fracture

Ignored

---

# Example

Point 1

Valid

Point 2

Valid

...

Point 842

Fracture

Point 843

Ignored

Point 844

Ignored

...

---

# Engineering Rule

Raw arrays

are never modified.

Only

PointStatus()

and

FractureIndex

are generated.

---

# Validation

Fracture Index

>

0

Fracture Index

<

Point Count

Fracture Force

>

0

Fracture before end of dataset

---

# Error Codes

1501

No Fracture Found

1502

Dataset Too Short

1503

Invalid Force Array

1504

Invalid Crosshead Array

1505

Invalid Stress Array

---

# Performance

O(n)

Memory

Minimal

---

# Output Structure

Fracture

├── Index

├── Force

├── Stress

├── Extension

├── Strain

└── Detection Method

---

# Detection Method

Stored for audit.

Possible values

Automatic

Manual

Imported

Administrator configurable.

---

# Manual Override

The operator may redefine

Fracture Point

by clicking the graph.

The original automatic result remains stored.

Both values are recorded.

---

# Engineering Rule

The engine

never

calculates

Young Modulus

Yield

Stress

Strain

Graph

Only

Fracture Detection

---

# Acceptance

✔ Array Based

✔ Non-destructive

✔ Manual Override

✔ Audit Compatible

✔ ISO 17025 Compatible

✔ Excel Independent

✔ SQLite Independent

---

End Of Document
