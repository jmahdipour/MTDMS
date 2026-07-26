# Strain Calculation Engine

Document ID

MTDMS-CAL-012

Version

1.0

Status

Core Engine

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Dependencies

EngineeringDataset

---

# Purpose

The Strain Engine calculates engineering strain for every sampled point.

The engine automatically selects the proper displacement source depending on the availability of the extensometer.

No worksheet access is permitted.

---

# Engineering Rule

Preferred source

Extensometer

Fallback source

Crosshead Displacement

The source shall be selected automatically.

---

# Input Sources

Case 1

Extensometer Connected

Input

EngineeringDataset.Raw.Extensometer()

----------------------------

Case 2

No Extensometer

Input

EngineeringDataset.Raw.Crosshead()

---

# Gauge Length

Input

EngineeringDataset.Metadata.GaugeLength

Current TXT File

L0

Metadata Line 13

---

# Formula

Engineering Strain

ε = ΔL / L0

where

ΔL

Extension

or

Crosshead

depending on availability.

---

# Units

Extension

mm

Gauge Length

mm

Output

Engineering Strain

dimensionless

---

# Optional Output

Engineering Strain (%)

```
ε%

=

ε ×100
```

This conversion is performed only for report generation.

Internal arrays remain dimensionless.

---

# Inputs

EngineeringDataset.Raw.Crosshead()

EngineeringDataset.Raw.Extensometer()

EngineeringDataset.Metadata.GaugeLength

EngineeringDataset.Flags.ExtensometerAvailable

---

# Outputs

EngineeringDataset.Calc.Strain()

---

# Preconditions

GaugeLength>0

Dataset Imported

Dataset Validated

---

# Source Selection

```
ExtensometerAvailable

↓

TRUE

↓

Use Extensometer


FALSE

↓

Use Crosshead
```

---

# Processing Algorithm

```
For every point

If ExtensometerAvailable

↓

Strain(i)

=

Extensometer(i)

/

GaugeLength

Else

↓

Strain(i)

=

Crosshead(i)

/

GaugeLength

```

---

# Pseudocode

```vb

If Dataset.Flags.ExtensometerAvailable Then

    For i = 1 To PointCount

        Strain(i)=Extensometer(i)/GaugeLength

    Next

Else

    For i = 1 To PointCount

        Strain(i)=Crosshead(i)/GaugeLength

    Next

End If

```

---

# Output Array

Index

↓

Strain(i)

Array length

=

Raw arrays

---

# Invalid Gauge Length

GaugeLength<=0

↓

Fatal Error

Abort Calculation

---

# Invalid Extension

Invalid Point

↓

Strain(i)=NaN

↓

Continue

---

# Memory Policy

Raw Arrays

Never Modified

Only

Calc.Strain()

is written.

---

# Validation

Check

Maximum Strain

Minimum Strain

NaN Count

Negative Values

Array Length

---

# Error Codes

1201

Gauge Length Missing

1202

Gauge Length Zero

1203

Input Array Missing

1204

Array Length Mismatch

---

# Engineering Rule

The Strain Engine

shall never

calculate

Stress

Young Modulus

Yield

Fracture

Graph Correction

These belong to separate engines.

---

# Unit Tests

Case 1

Gauge Length

50

Extension

5

↓

Strain

0.10

PASS

----------------------------

Case 2

Gauge Length

100

Crosshead

2

↓

Strain

0.02

PASS

----------------------------

Case 3

Gauge Length

0

↓

Abort

PASS

---

# Performance

Complexity

O(n)

Memory

One Double Array

---

# Acceptance

✔ Array Based

✔ Automatic Source Selection

✔ Double Precision

✔ No Worksheet Access

✔ No TXT Access

✔ No SQLite Access

✔ Dimensionless Output

✔ ISO 17025 Compatible

---

# Related Documents

CAL-011_StressEngine

CAL-013_YoungModulusEngine

CAL-014_YieldEngine

---

End Of Document
