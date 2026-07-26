# Young Modulus Calculation Engine

Document ID

MTDMS-CAL-013

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

Young Modulus Engine calculates the elastic modulus from the linear elastic region of the stress-strain curve.

The engine does not calculate yield strength.

The engine does not correct the graph.

It only identifies the elastic linear region and determines its slope.

---

# Engineering Principle

Young Modulus

E

=

Δσ

/

Δε

The modulus shall always be calculated from the largest valid linear region.

Never from only two points.

---

# Inputs

EngineeringDataset.Calc.Stress()

EngineeringDataset.Calc.Strain()

---

# Outputs

EngineeringDataset.Calc.YoungModulus

EngineeringDataset.Flags.LinearRegionFound

EngineeringDataset.LinearRegion.StartIndex

EngineeringDataset.LinearRegion.EndIndex

---

# Preconditions

Stress calculated

Strain calculated

Dataset validated

Minimum point count available

---

# Engineering Rule

Young Modulus is calculated only once.

Every other engine uses this value.

No engine recalculates Young Modulus.

---

# Linear Region Detection

The elastic region shall be determined before calculating the slope.

The linear region must satisfy:

• Continuous

• Increasing

• No unloading

• No fracture

• Maximum linearity

---

# Candidate Region

The engine searches only from

Beginning of the curve

↓

Until before yield

Fracture region is ignored.

---

# Regression

Linear Least Squares Regression

is used.

Not two-point slope.

---

# Output

Regression produces

Slope

Intercept

R²

Standard Error

Number of Points

---

# Acceptance Criteria

R²

shall be greater than the configurable limit.

Default

0.999

If not

↓

Search continues.

---

# Multiple Candidates

If several acceptable linear regions exist

↓

Choose the longest region.

If equal

↓

Choose the region with the highest R².

---

# Stored Results

Young Modulus

Regression R²

Start Point

End Point

Point Count

---

# Memory

Only

EngineeringDataset.Calc

is modified.

Stress

Strain

remain unchanged.

---

# Error Codes

1301

Stress Missing

1302

Strain Missing

1303

Insufficient Points

1304

Linear Region Not Found

1305

Regression Failed

---

# Validation

Young Modulus > 0

R² acceptable

Point Count acceptable

Slope finite

No NaN

---

# Unit

Input

Stress

kgf/mm²

Input

Strain

dimensionless

Output

Young Modulus

kgf/mm²

Unit conversion is handled only by Report Engine.

---

# Performance

Regression

O(n)

Search

O(n)

Memory

Minimal

---

# Engineering Rule

This engine never

Corrects Graph

Calculates Yield

Calculates True Stress

Detects Fracture

Only

Elastic Modulus

---

# Acceptance

✔ Array Based

✔ Regression Based

✔ Worksheet Independent

✔ TXT Independent

✔ SQLite Independent

✔ ISO 17025 Compatible

---

End Of Document
