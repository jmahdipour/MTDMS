# Young's Modulus Calculation Engine

Document ID : MTDMS-CE-006

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Input

TXT File

Application

MTDMS

Status

Production

---

# Purpose

The Young's Modulus Calculation Engine determines the elastic modulus (Young's Modulus, **E**) from the tensile test data imported from the TXT file.

The calculated value is used for engineering evaluation, graph correction, and reporting.

The engine shall also support comparison with reference values stored in the Material Property Library.

---

# Objectives

The Young's Modulus Engine shall

• Identify the elastic region

• Calculate Young's Modulus

• Validate elastic linearity

• Compare with reference values

• Supply graph correction data

---

# Engineering Philosophy

TXT File

↓

Engineering Stress

↓

Engineering Strain

↓

Elastic Region

↓

Young's Modulus

↓

Validation

↓

Graph Correction

Every calculation is derived from the imported TXT file.

Reference values never replace measured values.

---

# Engineering Definition

Young's Modulus is defined as

\[
E=\frac{\Delta \sigma}{\Delta \varepsilon}
\]

where

\[
\sigma = \text{Engineering Stress}
\]

\[
\varepsilon = \text{Engineering Strain}
\]

---

# Input Data

Engineering Stress

Engineering Strain

Gauge Length

Cross-sectional Area

Material Reference (optional)

Selected Standard

---

# Elastic Region Identification

The elastic region shall

• begin at the origin

• remain approximately linear

• terminate before yielding

The identified region is passed to the Yield Detection Engine and the Graph Correction Engine.

---

# Calculation Methods

The engine shall support

### Method 1

Linear Regression

Preferred

---

### Method 2

Two-Point Slope

When specified by the selected standard

---

### Method 3

User-Defined Region

Operator selects the elastic range manually

Administrator configurable.

---

# Reference Comparison

If a reference value exists in the Material Property Library

the engine shall calculate

Measured E

Reference E

Difference

Percentage Difference

No correction of measured values shall occur.

---

# Graph Correction

The calculated Young's Modulus may be used by the Graph Correction Engine to align the elastic portion of the stress–strain curve.

Only the displayed graph is corrected.

Engineering results remain unchanged.

---

# Output Data

Young's Modulus

Elastic Region Start

Elastic Region End

Regression Coefficient

Reference Comparison

Graph Correction Parameters

---

# Validation

Validation shall verify

Linearity

Minimum Number of Points

Reasonable Engineering Range

Standard Requirements

---

# Engineering Independence

The Young's Modulus Engine

shall never modify

Imported TXT

Engineering Stress

Engineering Strain

Measured Results

Only

derived values

are generated.

---

# SQLite Interaction

SQLite stores

Young's Modulus

Validation Status

Reference Comparison

Graph Correction Parameters

Intermediate calculations are not stored.

---

# Error Handling

Elastic Region Not Found

↓

Reject

Insufficient Points

↓

Reject

Poor Linearity

↓

Warning

Reference Missing

↓

Comparison Skipped

---

# Performance Targets

Elastic Region Detection

< 100 ms

Regression

< 100 ms

Reference Comparison

< 20 ms

---

# Acceptance Criteria

✔ Young's Modulus calculated

✔ Linear regression supported

✔ Manual selection supported

✔ Reference comparison supported

✔ Graph correction parameters generated

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO 6892-1 compatible

✔ ASTM E111 compatible

✔ ISO/IEC 17025 compliant

✔ Complete reproducibility from TXT

---

End of Document
