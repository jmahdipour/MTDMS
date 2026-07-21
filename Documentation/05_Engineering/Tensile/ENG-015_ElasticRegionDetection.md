# Elastic Region Detection

Document ID : MTDMS-ENG-015

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

This document defines the algorithm used to automatically detect the elastic region of the engineering stress–strain curve.

Accurate determination of the elastic region is the most important step because it directly affects

• Young's Modulus

• Offset Yield Strength

• Graph Correction

• ISO 6892 Compliance

A poor elastic-region selection propagates errors into every subsequent calculation.

---

# Reference Standards

ISO 6892-1

ASTM E111

ISO 7500-1

---

# Design Philosophy

The elastic region shall **not** be selected using a fixed percentage of maximum load.

Instead, it shall be detected from the actual behavior of the measured curve.

---

# Pipeline

```
Engineering Stress

↓

Engineering Strain

↓

Noise Filtering

↓

Linear Window Search

↓

Regression Analysis

↓

Best Linear Segment

↓

Elastic Region
```

---

# Input

Engineering Stress[]

Engineering Strain[]

Sampling Interval

Material Information

(Optional)

---

# Output

ElasticStartIndex

ElasticEndIndex

RegressionSlope

RegressionIntercept

RegressionR²

YoungMeasured

---

# Detection Strategy

The software searches for the **longest continuous linear segment** of the stress-strain curve.

Every candidate segment is evaluated.

The segment with the highest engineering quality score is selected.

---

# Candidate Window

Minimum Points

50

Recommended

100

Maximum

Dynamic

---

# Sliding Window Algorithm

```
Window

↓

Linear Regression

↓

Calculate R²

↓

Expand Window

↓

Repeat

↓

Store Best Candidate
```

---

# Selection Criteria

Primary

Highest R²

Secondary

Longest Window

Third

Lowest Standard Error

---

# Required R²

Minimum

0.9990

Preferred

0.9995

Excellent

0.9998

---

# Window Expansion

If

Regression Quality

Improves

↓

Expand

If

Regression Quality

Drops

↓

Stop Expansion

Store Previous Window

---

# Material Assistance

If Material Library contains

Young's Modulus

↓

Expected Elastic Slope

↓

Search starts around expected behavior

This improves robustness for noisy curves.

---

# Noise Rejection

Before regression

Optional smoothing

may be applied.

Allowed methods

Moving Average

Savitzky–Golay

Median Filter

Default

None

Raw data always preserved.

---

# Regression

Method

Ordinary Least Squares

Returns

Slope

Intercept

R²

Residual Error

---

# Acceptance Rules

The selected elastic region shall satisfy

Continuous

Linear

No Yield

No Necking

No Fracture

---

# Rejection Rules

Reject window if

Stress decreases

Large oscillation

Insufficient points

Negative slope

R² below minimum

---

# Manual Override

Operator may manually select

Start

End

of elastic region.

Manual selection

↓

Recalculate Young's Modulus

↓

Recalculate Offset Yield

↓

Update Graph

Raw data remains unchanged.

---

# Storage

SQLite

Table

```
tblEngineeringResult
```

Fields

ElasticStartIndex

ElasticEndIndex

RegressionSlope

RegressionIntercept

RegressionR2

ElasticMethod

Automatic

Manual

---

# Graph Visualization

The elastic region shall be highlighted.

Displayed

Green Line

Operator may verify visually.

Guide lines shall not appear in the final report.

---

# Error Conditions

No acceptable window found

↓

Engineering Error

Window too short

↓

Warning

Regression failed

↓

Abort

NaN detected

↓

Abort

---

# Performance

Algorithm

Sliding Window Regression

Complexity

Approximately O(n)

Suitable for

100,000 samples

---

# Future Improvements

Adaptive Window Size

Machine Learning Detection

Robust Regression

Outlier Elimination

Automatic Elastic-End Detection

Reserved

---

# Acceptance Criteria

✔ Complies with ASTM E111 philosophy

✔ Compatible with ISO 6892-1

✔ Automatically finds the best linear region

✔ Supports manual override

✔ Uses regression

✔ Stores complete regression information

✔ Excel 2019 compatible

✔ SQLite compatible

---

End of Document
