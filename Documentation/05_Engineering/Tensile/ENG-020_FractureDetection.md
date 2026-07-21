# Fracture Detection Algorithm

Document ID : MTDMS-ENG-020

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Engineering → Tensile

Status

Production

---

# Purpose

This document defines the automatic fracture detection algorithm.

The fracture point determines

• End of Engineering Curve

• End of True Stress-Strain Curve

• Elongation After Fracture

• Reduction of Area

• Graph Termination

• Report Generation

No engineering calculation shall continue beyond the fracture point.

---

# Reference Standards

ISO 6892-1

ASTM E8 / ASTM E8M

ISO 7500-1

---

# Definition

Fracture occurs when the specimen separates into two pieces and the applied load rapidly decreases toward zero.

The Import Engine shall identify the fracture point automatically.

---

# Detection Philosophy

Engineering Curve

↓

Ultimate Strength

↓

Necking

↓

Rapid Load Drop

↓

Fracture

↓

Stop

---

# Input Data

Force[]

Engineering Stress[]

Engineering Strain[]

Stroke[]

Extension[]

Time[]

---

# Output

Fracture Index

Fracture Force

Fracture Stress

Fracture Extension

Fracture Time

Fracture Status

---

# Detection Pipeline

```
Engineering Stress

↓

Engineering Force

↓

Locate UTS

↓

Search After UTS

↓

Rapid Load Drop

↓

Confirm Fracture

↓

Store Results
```

---

# Primary Criterion

A fracture event is detected when

Force decreases rapidly

and

does not recover.

---

# Recommended Threshold

```
Force Drop

>

90 %

within

10 Samples
```

Administrator configurable.

---

# Secondary Criterion

After fracture

Force remains

approximately zero.

Recovery above threshold

means

Not Fracture.

---

# Third Criterion

Engineering Stress

Monotonically decreases

until

Near Zero.

---

# Validation

Fracture

Must occur

After

UTS

---

```
Fracture Index

>

UTS Index
```

---

# False Fracture Rejection

Ignore

Temporary Noise

Temporary Slip

Grip Movement

Signal Spike

Machine Vibration

---

# Noise Filter

Optional

Moving Average

Median Filter

Savitzky–Golay

Default

Disabled

Raw Data

Never Modified

---

# Manual Override

Operator

May manually

Select

Fracture Point

↓

Engineering Results

Updated

↓

Audit Logged

---

# Graph Behaviour

Graph

Terminates

Exactly

At

Fracture Index

No points shall be displayed after fracture.

---

# Engineering Behaviour

True Stress

Stops

Engineering Strain

Stops

Plastic Analysis

Stops

Statistics

Continue

Only using valid data.

---

# Error Conditions

No Fracture Found

↓

Warning

Use Last Valid Sample

Fracture Before UTS

↓

Engineering Error

Negative Force

↓

Validation

Overflow

↓

Abort

Rollback

---

# SQLite Storage

Table

```
tblEngineeringResult
```

Fields

FractureIndex

FractureForce

FractureStress

FractureExtension

FractureTime

DetectionMethod

Automatic

Manual

---

# Performance

Complexity

```
O(n)
```

Single pass

after

UTS

---

# Future Improvements

Machine Learning Detection

Acoustic Fracture Recognition

Video Synchronization

Digital Image Correlation

Reserved

---

# Acceptance Criteria

✔ Fracture always after UTS

✔ Automatic detection

✔ Manual override

✔ Graph terminates correctly

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO 6892-1 compliant

---

End of Document
