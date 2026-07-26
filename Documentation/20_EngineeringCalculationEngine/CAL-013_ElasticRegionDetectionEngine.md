# Elastic Region Detection Engine

Document ID

MTDMS-CAL-013

Version

1.0

Status

Core Engine

Platform

Excel 2019 VBA

Application

MTDMS

Dependencies

EngineeringDataset

---

# Purpose

The Elastic Region Detection Engine automatically identifies the elastic region of the engineering stress-strain curve.

This engine is the foundation for

• Young Modulus

• Offset Yield

• Graph Correction

Without a correct elastic region every subsequent engineering result becomes inaccurate.

---

# Engineering Principle

The elastic region is the longest continuous portion of the stress-strain curve exhibiting linear behavior.

It is **not** necessarily located between the first and second points.

It is **not** assumed.

It must be detected.

---

# Inputs

EngineeringDataset.Calc.Stress()

EngineeringDataset.Calc.Strain()

---

# Outputs

ElasticStartIndex

ElasticEndIndex

ElasticSlope

ElasticIntercept

RegressionCoefficient

ElasticMask()

---

# Output Objects

```vb
ElasticStartIndex As Long

ElasticEndIndex As Long

ElasticSlope As Double

ElasticIntercept As Double

RegressionR2 As Double

ElasticMask() As Boolean
```

---

# Processing Pipeline

EngineeringDataset

↓

Stress()

↓

Strain()

↓

Sliding Window

↓

Linear Regression

↓

Best Linear Segment

↓

Elastic Region

---

# Detection Method

The engine does NOT fit one line to the entire curve.

Instead

```
Window

↓

Regression

↓

Move Window

↓

Regression

↓

Move Window

↓

Regression
```

The best linear region is selected.

---

# Sliding Window

Recommended

Minimum Window

30 Points

Maximum Window

Administrator configurable

Default

50 Points

---

# Linear Regression

For each window

Compute

Slope

Intercept

R²

Standard Error

Residual

---

# Selection Criteria

Primary

Maximum R²

Secondary

Maximum Continuous Length

Third

Minimum Standard Error

---

# Engineering Constraints

Elastic region

must begin after preload

must end before yielding

must not include fracture

must not include unloading

---

# Accepted Region

```
Stress

│

│

│

│        Linear

│      /

│    /

│  /

│/

└────────────────────

Strain
```

---

# Rejected Regions

Yield Plateau

Plastic Zone

Fracture

Machine Slack

---

# Pseudocode

```vb
For Window = Start To End

    Calculate Linear Regression

    Calculate R²

    If Better Region Then

        Save Region

    End If

Next
```

---

# Quality Metrics

Slope

Intercept

R²

Residual Error

Point Count

---

# Default Acceptance

R²

≥ 0.999

Administrator configurable.

---

# Memory

Creates

ElasticMask()

One Boolean Array

---

# Validation

ElasticStartIndex

<

ElasticEndIndex

Point Count

>

Minimum Window

Slope

>

0

---

# Error Codes

1301

No Linear Region

1302

Regression Failed

1303

Window Too Small

1304

Dataset Too Short

---

# Engineering Rule

This engine

shall never calculate

Young Modulus

Yield

Fracture

Graph Correction

It only detects

Elastic Region.

---

# Unit Tests

Case

Ideal Linear Curve

↓

PASS

------------------------

Case

Linear + Plastic

↓

PASS

------------------------

Case

Only Plastic

↓

FAIL

------------------------

Case

Noise

↓

PASS

If R² acceptable

---

# Performance

Complexity

O(n)

Sliding Regression

Optimized

---

# Acceptance

✔ Automatic Detection

✔ Array Based

✔ Regression Based

✔ Noise Resistant

✔ High Precision

✔ Excel Independent

✔ ISO 6892 Compatible

---

# Related Documents

CAL-014_YoungModulusEngine

CAL-015_GraphCorrectionEngine

CAL-016_YieldDetectionEngine

---

End Of Document
