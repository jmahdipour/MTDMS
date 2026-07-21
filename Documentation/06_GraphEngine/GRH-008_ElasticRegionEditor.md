# Elastic Region Editor

Document ID : MTDMS-GRH-008

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Graph Engine

Status

Production

---

# Purpose

This document defines the Elastic Region Editor.

The Elastic Region Editor allows the operator to verify and adjust the elastic portion of the tensile curve before Young's Modulus calculation and graph correction.

This module is one of the most critical engineering tools because every subsequent calculation depends on the correct identification of the elastic region.

---

# Reference Standards

ISO 6892-1

ASTM E111

ISO 7500-1

ISO 17025

---

# Engineering Definition

The elastic region is the portion of the stress-strain curve in which

Stress

is proportional to

Strain.

Within this region

Hooke's Law applies.

```
σ = E × ε
```

---

# Scope

The editor is used for

Young's Modulus

Elastic Limit

Yield Verification

Graph Correction

Compliance Verification

---

# Workflow

Import Test

↓

Automatic Elastic Region Detection

↓

Display Region

↓

Operator Review

↓

Modify Region

↓

Recalculate Young's Modulus

↓

Approve

↓

Store

---

# Automatic Detection

The software initially detects

the largest linear segment

using

Linear Regression.

The detected region is highlighted.

---

# Operator Editing

The operator may adjust

Start Point

End Point

Entire Region

using the mouse.

The region boundaries shall always remain on the engineering curve.

---

# Editing Constraints

Start

must occur

after

Zero Point

End

must occur

before

Yield Point

```
Zero

↓

Elastic

↓

Yield

↓

Plastic
```

---

# Live Update

During editing

the following values shall be recalculated continuously

Young's Modulus

Regression R²

Elastic Length

Elastic Stress Range

Elastic Strain Range

---

# Regression

The selected region is evaluated using

Least Squares Linear Regression.

Outputs

Slope

Intercept

Coefficient of Determination

```
R²
```

---

# Acceptance Threshold

Default

```
R² ≥ 0.9990
```

Warning

```
0.995 ≤ R² < 0.999
```

Reject

```
R² < 0.995
```

Administrator configurable.

---

# Display

Elastic Region

Blue Highlight

Regression Line

Green

Excluded Data

Gray

Selected Endpoints

Large Blue Markers

---

# Context Menu

Approve

Reset Automatic

Expand Region

Shrink Region

Recalculate

Copy Results

Properties

---

# Keyboard Shortcuts

Left Arrow

Move Start

Right Arrow

Move End

Ctrl + Arrow

Fine Adjustment

Enter

Approve

Esc

Cancel

---

# Validation Rules

Elastic Region

must contain

at least

30 samples.

Preferred

100 samples.

The region shall not overlap

Plastic Region.

---

# Database Storage

SQLite

Table

```
tblElasticRegion
```

Fields

ElasticStartIndex

ElasticEndIndex

YoungModulus

RegressionSlope

RegressionIntercept

RegressionR2

Operator

Timestamp

Approved

---

# Report Behaviour

Engineering Report

Displays

Approved Elastic Region

Young's Modulus

Regression Line

Regression R²

Construction lines used during editing

shall not appear.

---

# Error Handling

Region Too Small

↓

Reject

Region After Yield

↓

Engineering Error

Regression Failure

↓

Abort

Invalid Sample Order

↓

Reject

---

# Future Enhancements

Automatic Multi-Region Search

AI Elastic Region Selection

Robust Regression

Outlier Rejection

Compliance Compensation Integration

Reserved

---

# Acceptance Criteria

✔ Elastic region editable

✔ Real-time regression

✔ Real-time Young's Modulus

✔ R² validation

✔ Undo / Redo

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO 17025 traceability

✔ Original data never modified

---

End of Document
