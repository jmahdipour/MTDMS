# TXT Graph Data Preparation

Document ID : MTDMS-IMP-030

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Database

SQLite

---

# Purpose

This document defines how imported engineering data is prepared for graph generation.

The Graph Engine never reads TXT files directly.

The Graph Engine never calculates engineering values.

Its only responsibility is preparing optimized graph datasets.

---

# Architecture

TXT

↓

Parser

↓

Raw Data

↓

Engineering Engine

↓

Engineering Data

↓

Graph Preparation

↓

Chart Engine

↓

Operator

---

# Philosophy

Raw Data

↓

Engineering Data

↓

Graph Dataset

↓

Charts

Graph preparation never modifies engineering values.

---

# Graph Preparation Pipeline

Engineering Data

↓

Sorting

↓

Cleaning

↓

Fracture Detection

↓

Visible Range

↓

Marker Creation

↓

Graph Dataset

---

# Graph Dataset

Each graph receives

X Values

Y Values

Marker Positions

Annotations

Display Limits

Axis Labels

Units

---

# Graph Types

Engineering Stress vs Engineering Strain

True Stress vs True Strain

Force vs Stroke

Force vs Extension

Stress vs Time

Force vs Time

Extension vs Time

Machine Displacement

Future

Custom Graphs

---

# Graph Source

Always

```
tblEngineeringData
```

Never

```
tblRawData
```

Except

Raw View Mode

---

# Sorting

Graph data sorted by

Time

or

Engineering Strain

depending on graph type.

---

# Data Cleaning

Remove

Invalid Samples

Duplicate Samples

Ignored Samples

Filtered Samples

Keep

Valid Engineering Samples

---

# Fracture Detection

Engineering Engine supplies

Fracture Index

Graph Engine

Cuts graph

Exactly at fracture point.

No data after fracture displayed.

---

# Elastic Region

Engineering Engine supplies

Elastic Region Start

Elastic Region End

Graph Engine highlights

Elastic Region

---

# Yield Marker

Engineering Engine supplies

Yield Position

Graph Engine displays

Yield Marker

Operator may move marker

if Manual Mode enabled.

---

# Ultimate Tensile Strength Marker

Graph displays

UTS

Automatically.

---

# Fracture Marker

Graph displays

Fracture

Automatically.

---

# Necking Marker

Future

Supported

Reserved.

---

# Axis Preparation

X Axis

Depends on graph

Examples

Engineering Strain

True Strain

Stroke

Extension

Time

---

Y Axis

Engineering Stress

True Stress

Force

Temperature

Speed

---

# Units

Taken from

Internal Engineering Units

Never original TXT units.

---

# Scaling

Automatic

↓

Zoom to valid data

↓

Include fracture

↓

No empty trailing region

---

# Graph Resolution

Every engineering sample

↓

One graph point

No interpolation.

---

# Large Dataset Strategy

Over

100000 Samples

↓

Graph Decimation

Display Only

Engineering Data remains unchanged.

---

# Graph Cache

Prepared graph datasets

Stored in memory

During active session.

No recalculation unless Engineering Data changes.

---

# SQLite

Graph preparation

Does NOT store

Prepared graph arrays.

Only engineering values stored.

---

# Future Graph Layers

Elastic Region

Plastic Region

Yield Offset Line

Young's Modulus Line

Moving Average

Noise Filter

Reserved.

---

# Acceptance Criteria

✔ Graph uses Engineering Data only

✔ Fracture automatically limits graph

✔ Yield marker available

✔ UTS marker available

✔ Automatic scaling

✔ Compatible with Excel Charts

✔ Supports 100000+ samples

---

End of Document
