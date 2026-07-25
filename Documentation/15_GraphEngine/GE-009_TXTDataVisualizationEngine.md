# TXT Data Visualization Engine

Document ID : MTDMS-GE-009

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

The TXT Data Visualization Engine provides direct visualization of the **raw data imported from the testing machine TXT file**, before any engineering calculations or graph corrections are applied.

This allows the operator to inspect the original acquisition data exactly as exported by the testing machine.

The raw graph is intended for verification, troubleshooting, and engineering review.

---

# Objectives

The TXT Data Visualization Engine shall

• Display the original imported dataset

• Preserve the original measurement order

• Detect acquisition anomalies

• Compare raw and engineering graphs

• Support laboratory verification

---

# Engineering Philosophy

Machine TXT File

↓

Raw Dataset

↓

Raw Visualization

↓

Engineering Calculation

↓

Engineering Graph

The raw graph shall always represent the original machine output.

---

# Data Source

Only

Imported TXT File

No calculated values

No corrected values

No reconstructed values

No filtered values

---

# Supported Raw Graphs

Force vs Time

Force vs Crosshead Displacement

Force vs Extensometer Extension

Crosshead Position vs Time

Extensometer vs Time

Load Cell Output

Machine Channel Data

Administrator configurable.

---

# Graph Workflow

```
TXT File

↓

TXT Parser

↓

Raw Dataset

↓

Excel Chart

↓

Operator Inspection
```

---

# Raw Dataset Integrity

The engine shall preserve

Original Point Order

Original Sampling Frequency

Original Resolution

Original Measurement Precision

No smoothing is permitted.

---

# Available Channels

Depending on the imported TXT file

Force

Crosshead Position

Extensometer

Time

Machine Speed

Load Cell Number

Digital Inputs

Digital Outputs

Analog Channels

Temperature (future)

Additional channels shall be imported automatically when recognized.

---

# Multi-Channel Display

The operator may display

Single Channel

Dual Channel

Multiple Channels

Shared Time Axis

Separate Axes

Administrator configurable.

---

# Channel Visibility

Each imported channel may be

Visible

Hidden

Renamed

Reordered

Grouped

without modifying the original dataset.

---

# Acquisition Inspection

The operator may inspect

Sampling Gaps

Signal Noise

Dropped Samples

Load Cell Switching

Signal Saturation

Machine Stops

Communication Interruptions

These inspections do not modify the dataset.

---

# Comparison Mode

The engine shall support

Raw Graph

↓

Engineering Graph

↓

Overlay Comparison

This feature assists in verifying engineering calculations and graph corrections.

---

# Export

The raw graph may be exported as

Excel Chart

PNG

EMF

PDF

The exported graph shall clearly indicate

**RAW MACHINE DATA**

to prevent confusion with corrected engineering graphs.

---

# Engineering Independence

The TXT Data Visualization Engine

shall never

calculate

Stress

Strain

Young's Modulus

Yield Strength

True Stress

True Strain

It displays only imported machine data.

---

# SQLite Interaction

SQLite stores

Display Preferences

Visible Channels

Graph Configuration

Operator Preferences

The raw dataset itself continues to originate from the TXT file.

---

# Error Handling

TXT Missing

↓

Abort

Unsupported Channel

↓

Ignore

Corrupted Dataset

↓

Abort

Missing Force Channel

↓

Warning

Invalid Sampling Order

↓

Warning

---

# Performance Targets

Typical Raw Dataset

Display

< 300 ms

Large Dataset

100,000 Points

< 2 s

Channel Switching

Immediate

---

# Acceptance Criteria

✔ Raw TXT visualization supported

✔ Multi-channel display supported

✔ Original sampling preserved

✔ Overlay with engineering graph supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability to original TXT file

---

End of Document
