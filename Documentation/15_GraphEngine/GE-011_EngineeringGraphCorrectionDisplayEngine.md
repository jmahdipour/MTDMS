# Engineering Graph Correction Display Engine

Document ID : MTDMS-GE-011

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Chart Technology

Microsoft Excel Chart Objects

Database

SQLite

Primary Data Source

TXT File (Testing Machine Export)

Application

MTDMS

Status

Production

---

# Purpose

The Engineering Graph Correction Display Engine visually presents engineering graph corrections without modifying the original engineering dataset.

Its purpose is to allow the operator to compare the original graph with the visually corrected graph used for engineering interpretation.

The corrected graph is a **display layer only**.

---

# Objectives

The Graph Correction Display Engine shall

• Display corrected engineering graphs

• Compare corrected and original graphs

• Preserve engineering calculations

• Display correction references

• Support engineering verification

---

# Engineering Philosophy

Original Engineering Dataset

↓

Graph Correction Parameters

↓

Corrected Display

↓

Engineering Review

The displayed graph may change.

The engineering data never change.

---

# Supported Corrections

Elastic Region Alignment

Horizontal Offset Removal

Origin Alignment

Fracture Trimming

Display Scaling

Marker Optimization

Reference Modulus Alignment

Administrator configurable.

---

# Workflow

```
TXT File

↓

Engineering Dataset

↓

Correction Parameters

↓

Display Transformation

↓

Corrected Graph
```

---

# Display Layers

Layer 1

Original Engineering Curve

----------------------------

Layer 2

Corrected Engineering Curve

----------------------------

Layer 3

Reference Construction Lines

----------------------------

Layer 4

Engineering Markers

The operator may enable or disable each layer independently.

---

# Elastic Alignment

The corrected display shall align the elastic portion of the graph with the calculated Young's Modulus.

Only the display coordinates are transformed.

Engineering stress and strain remain unchanged.

---

# Horizontal Offset

The engine may remove

Grip Seating

Machine Slack

Initial Contact Offset

from the displayed graph.

The imported measurements remain unchanged.

---

# Fracture Display

The corrected graph may terminate at the detected fracture point.

The original graph may continue to display the remaining imported data if requested.

---

# Construction Lines

Temporary engineering construction lines include

Elastic Regression

Offset Line

Reference Modulus

Yield Construction

These lines shall

not appear

in the final report

unless explicitly enabled.

---

# Comparison Mode

Supported

Original Only

Corrected Only

Overlay

Split View (future)

Administrator configurable.

---

# Engineering Verification

The operator may switch instantly between

Original

Corrected

Overlay

to verify that

engineering calculations remain identical.

---

# Engineering Independence

The Graph Correction Display Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Only chart coordinates are transformed for display.

---

# SQLite Interaction

SQLite stores

Display Preferences

Correction Visibility

Operator Preferences

No transformed engineering data are stored.

---

# Error Handling

Missing Correction Parameters

↓

Display Original

Missing Young's Modulus

↓

Skip Elastic Alignment

Invalid Transformation

↓

Reject

Chart Creation Failure

↓

Retry

---

# Performance Targets

Display Transformation

< 200 ms

Overlay Refresh

< 300 ms

Layer Toggle

Immediate

---

# Acceptance Criteria

✔ Corrected display supported

✔ Original display preserved

✔ Overlay comparison supported

✔ Construction lines configurable

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete reproducibility from TXT

---

End of Document
