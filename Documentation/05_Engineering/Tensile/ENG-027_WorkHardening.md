# Work Hardening Analysis

Document ID : MTDMS-ENG-027

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

This document defines the analysis of strain hardening (work hardening) during tensile testing.

Work hardening describes the increase in flow stress caused by plastic deformation.

The analysis is used for

• Material characterization

• Flow curve generation

• Finite Element material models

• Plastic deformation studies

• Research applications

---

# Reference Standards

ISO 6892-1

ASTM E8 / ASTM E8M

ASTM E111

---

# Definition

After yielding,

plastic deformation causes an increase in dislocation density.

This increases the stress required for further deformation.

This phenomenon is called

Work Hardening

or

Strain Hardening.

---

# Analysis Region

```
Yield

↓

Uniform Plastic Region

↓

Ultimate Tensile Strength
```

The work hardening analysis shall only use

Uniform Plastic Deformation.

Necking region

is excluded.

---

# Input Data

True Stress

True Strain

Yield Index

Necking Index

---

# Output

Hardening Curve

Hardening Rate

Hardening Exponent

Flow Curve Parameters

---

# Instantaneous Hardening Rate

The work hardening rate is

```
Θ

=

dσtrue

/

dεtrue
```

Units

MPa

---

# Numerical Differentiation

Central Difference

preferred

Forward Difference

Beginning

Backward Difference

End

---

# Hollomon Equation

The software shall support

```
σ

=

K εⁿ
```

Where

σ

True Stress

ε

True Plastic Strain

K

Strength Coefficient

n

Strain Hardening Exponent

---

# Linearized Form

Regression performed on

```
ln(σ)

=

ln(K)

+

n ln(ε)
```

Outputs

K

n

Regression R²

---

# Ludwik Model

Future Version

```
σ

=

σ₀

+

K εⁿ
```

Reserved

---

# Swift Model

Future Version

```
σ

=

K(ε₀+ε)^n
```

Reserved

---

# Voce Model

Future Version

Supported

Reserved

---

# Hardening Region Validation

Start

Yield

End

Before Necking

Minimum Points

100

Preferred

200

---

# Regression Quality

Minimum

```
R² ≥ 0.995
```

Preferred

```
R² ≥ 0.998
```

---

# Calculated Parameters

Strength Coefficient

K

Hardening Exponent

n

Regression R²

Maximum Hardening Rate

Average Hardening Rate

---

# Graph Representation

Display

True Stress

True Plastic Strain

Regression Line

Residual Error

Hardening Rate

Optional

---

# SQLite Storage

Table

```
tblWorkHardening
```

Fields

HardeningCoefficient

HardeningExponent

RegressionR2

MaximumHardeningRate

AverageHardeningRate

Model

---

# Error Conditions

Insufficient Plastic Data

↓

Abort

Necking Before Yield

↓

Engineering Error

Regression Failure

↓

Abort

NaN

↓

Abort

---

# Future Material Models

Hollomon

Implemented

Ludwik

Reserved

Swift

Reserved

Voce

Reserved

Johnson-Cook

Reserved

Ramberg-Osgood

Reserved

---

# Engineering Applications

Finite Element Material Card

Plastic Simulation

Metal Forming

Springback Analysis

Crash Simulation

Material Comparison

---

# Acceptance Criteria

✔ ISO 6892 compatible

✔ Uses True Stress–True Strain

✔ Excludes necking

✔ Calculates K and n

✔ Regression quality verified

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Ready for FEA export

---

End of Document
