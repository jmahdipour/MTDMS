# Vector Mathematics Library

Document ID : MTDMS-CAL-002

Version : 1.0

Status

Core Library

Platform

Excel 2019

Language

VBA

Primary Dataset

EngineeringDataset

Application

MTDMS

---

# Purpose

The Vector Mathematics Library provides high-performance mathematical operations on one-dimensional engineering arrays.

Every engineering calculation inside MTDMS shall use these vector functions.

The library never performs engineering calculations.

It only performs mathematical operations.

---

# Design Philosophy

Input

↓

Array

↓

Vector Function

↓

Array

↓

Engineering Engine

---

# Supported Data Types

Double()

Long()

Boolean()

String() (limited)

---

# Array Rules

Every vector must

• Start from index 1

• Be continuous

• Have identical length when paired

Example

Force(1...n)

Stress(1...n)

Time(1...n)

Crosshead(1...n)

---

# Library Structure

Math_Vector

Math_Array

Math_Search

Math_Filter

Math_Statistics

---

# Basic Operations

## Copy

```vb
Vec_Copy(Source(), Destination())
```

---

## Clear

```vb
Vec_Clear(Array())
```

---

## Fill

```vb
Vec_Fill(Array(), Value)
```

---

## Clone

```vb
NewArray = Vec_Clone(Source())
```

---

# Arithmetic

## Addition

```vb
Result = A + B
```

```vb
Vec_Add(A(), B(), Result())
```

---

## Subtraction

```vb
Vec_Subtract()
```

---

## Multiplication

```vb
Vec_Multiply()
```

---

## Division

```vb
Vec_Divide()
```

Division by zero

↓

Error Code

---

## Multiply by Constant

```vb
Vec_MultiplyScalar()

Force

↓

Stress
```

---

## Add Constant

```vb
Vec_AddScalar()
```

---

# Comparison

Equal

Greater

Less

Maximum

Minimum

---

# Mathematical Functions

Absolute

Square

Square Root

Power

Log

Ln

Exp

Sin

Cos

Tan

Administrator configurable

---

# Searching

Maximum Value

Minimum Value

Nearest Value

First Non-Zero

Last Non-Zero

Peak

Valley

---

# Index Functions

Maximum Index

Minimum Index

Nearest Index

Peak Index

Break Index

---

# Statistics

Mean

Median

Variance

Standard Deviation

Range

---

# Boolean Operations

Mask

AND

OR

NOT

---

# Example

Force()

↓

Maximum Force

```vb
MaxForce = Vec_Max(Force())
```

---

Crosshead()

↓

Maximum Extension

```vb
MaxExtension = Vec_Max(Crosshead())
```

---

# Return Types

Every function returns

Double

Long

Boolean

Array

No Variant.

---

# Error Codes

0

Success

--------------

1001

Length Mismatch

--------------

1002

Division By Zero

--------------

1003

Null Array

--------------

1004

Invalid Index

--------------

1005

Out Of Memory

---

# Memory Rules

No Worksheet

No Cells

No Range

Everything occurs inside RAM.

---

# Performance

Vector Addition

O(n)

Maximum

O(n)

Clone

O(n)

Clear

O(n)

---

# VBA Module

Recommended

```
modVectorMath
```

---

# Naming Convention

```
Vec_Copy

Vec_Clear

Vec_Add

Vec_Subtract

Vec_Max

Vec_Min

Vec_Search

Vec_Mean

Vec_STD
```

---

# Engineering Independence

This library never calculates

Stress

Strain

Yield

Young Modulus

Those belong to

Engineering Calculation Engine.

---

# Acceptance

✔ Array Based

✔ High Performance

✔ Double Precision

✔ Excel Independent

✔ SQLite Independent

✔ Engineering Independent

✔ Reusable

---

End Of Document
