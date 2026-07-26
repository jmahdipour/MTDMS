# Yield Strength Engine

Document ID

MTDMS-CAL-014

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

Young Modulus Engine

---

# Purpose

The Yield Strength Engine determines the yield point according to the method selected by the user.

The engine does not calculate Young Modulus.

The engine does not modify the graph.

It only determines the yield point.

---

# Engineering Principle

The Yield Engine shall never assume a single universal definition of yield.

Different materials require different methods.

Therefore the engine must operate according to the selected method.

---

# Supported Methods

Upper Yield

Lower Yield

Rp0.2

Rp0.1

Rp0.05

Rt0.5

Rt

Manual

Future Methods

---

# User Selection

Default

Rp0.2

The operator may change the method.

No automatic switching is allowed.

---

# Input

EngineeringDataset.Calc.Stress()

EngineeringDataset.Calc.Strain()

EngineeringDataset.Calc.YoungModulus

---

# Output

Yield Stress

Yield Strain

Yield Index

Yield Method

---

# Common Output Structure

Yield

├── Stress

├── Strain

├── Point Index

├── Method

└── Valid

---

# Method 1

Upper Yield

Definition

First local maximum before yielding.

---

# Method 2

Lower Yield

Definition

First stable minimum after upper yield.

---

# Method 3

Rp0.2

Definition

Intersection of

Stress-Strain Curve

and

Offset Line

Offset

0.2%

Parallel to Young Modulus.

---

# Method 4

Rp0.1

Offset

0.1%

---

# Method 5

Rp0.05

Offset

0.05%

---

# Method 6

Rt0.5

Permanent extension

0.5%

---

# Method 7

Rt

Total Extension

---

# Method 8

Manual

Operator selects

one point

on graph.

The coordinates become the yield point.

---

# Engineering Rule

The engine shall never decide

which method to use.

Only the Settings determine the active method.

---

# Calculation Flow

Read Method

↓

Call Dedicated Algorithm

↓

Return Yield Point

↓

Store Result

---

# Strategy Pattern

Yield Engine

↓

Upper Yield Engine

↓

Lower Yield Engine

↓

Rp Engine

↓

Rt Engine

↓

Manual Engine

---

# Validation

Yield Stress > 0

Yield Index valid

Yield before Maximum Force

Yield before Fracture

---

# Error Codes

1401

Young Modulus Missing

1402

Stress Missing

1403

Strain Missing

1404

Yield Not Found

1405

Manual Point Missing

---

# Performance

O(n)

Memory

Minimal

---

# Engineering Rule

The Yield Engine

never

changes graph

changes arrays

calculates modulus

detects fracture

Only

returns the yield point.

---

# Acceptance

✔ Strategy Based

✔ Manual Selection Supported

✔ ISO Ready

✔ ASTM Ready

✔ Array Based

✔ Worksheet Independent

✔ TXT Independent

✔ SQLite Independent

✔ Future Expandable

---

End Of Document
