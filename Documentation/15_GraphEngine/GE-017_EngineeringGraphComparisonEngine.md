# Engineering Graph Comparison Engine

Document ID : MTDMS-GE-017

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

The Engineering Graph Comparison Engine enables engineers to compare multiple engineering tests and visualize their similarities and differences without altering the original engineering datasets.

The comparison is performed using validated results reconstructed from the original TXT files.

The engine performs **no engineering calculations**.

---

# Objectives

The Graph Comparison Engine shall

• Compare multiple engineering graphs

• Compare engineering results visually

• Support historical comparison

• Support batch comparison

• Preserve engineering integrity

---

# Engineering Philosophy

TXT File A

↓

Engineering Dataset A

----------------------------

TXT File B

↓

Engineering Dataset B

----------------------------

Comparison Engine

↓

Comparison Graph

Each dataset preserves its engineering identity.

---

# Supported Comparisons

Current Test vs Previous Test

Batch vs Batch

Heat vs Heat

Material vs Material

Machine vs Machine

Operator vs Operator

Standard vs Standard

Reference vs Measured

Administrator configurable.

---

# Comparison Workflow

```
Engineering Dataset A

↓

Engineering Dataset B

↓

Alignment

↓

Comparison

↓

Engineering Review
```

---

# Alignment Modes

Supported

Origin

Maximum Force

Yield Point

Reference Strain

Reference Stress

Time

Manual

Administrator configurable.

Alignment affects only visualization.

---

# Curve Display

Each compared curve shall retain

Color

Legend

Material

Report Number

Test Date

Standard

Machine

Operator

---

# Difference Display

Optional

Difference Curve

Distance Between Curves

Maximum Difference

Average Difference

Area Difference

Reference Offset

These values are informational only.

---

# Statistical Comparison

The engine may compare

Young's Modulus

Yield Strength

Ultimate Strength

Elongation

Spring Constant

Ring Stiffness

Compression Strength

using values already calculated by the Calculation Engine.

---

# Historical Database

Comparisons may use

Current Test

Previous Tests

Selected Date Range

Selected Customer

Selected Material

Selected Batch

SQLite provides the historical records.

---

# Visual Indicators

The engine may highlight

Maximum Difference

Matching Region

Yield Difference

Fracture Difference

Reference Region

Administrator configurable.

---

# Report Support

Comparison graphs may be inserted into

Engineering Reports

Certificates

Laboratory Reports

Presentations

PDF

Administrator configurable.

---

# Engineering Independence

The Graph Comparison Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Only visual comparison is performed.

---

# SQLite Interaction

SQLite stores

Comparison History

Selected Datasets

Comparison Preferences

Operator

Timestamp

Engineering values remain unchanged.

---

# Error Handling

Missing Dataset

↓

Abort

Different Units

↓

Reject

Different Test Types

↓

Warning

Invalid Alignment

↓

Ignore

---

# Performance Targets

Two Curves

< 200 ms

Ten Curves

< 1 s

Historical Comparison

< 2 s

---

# Acceptance Criteria

✔ Engineering graph comparison supported

✔ Historical comparison supported

✔ Multiple alignment modes supported

✔ Statistical comparison supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability from TXT

---

End of Document
