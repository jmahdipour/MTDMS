# Engineering Dataset Class

Document ID

MTDMS-CAL-003

Version

1.0

Status

Core Object

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

---

# Purpose

EngineeringDataset is the core object exchanged between every subsystem inside MTDMS.

It contains

• Metadata

• Raw Data

• Calculated Data

• Flags

• Statistics

Every Engine receives exactly one EngineeringDataset object.

---

# Object Diagram

EngineeringDataset

├── Metadata

├── RawData

├── CalculatedData

├── Flags

├── Statistics

└── Methods

---

# Class Name

```vb
clsEngineeringDataset
```

---

# Internal Objects

```vb
clsMetadata

clsRawData

clsCalculatedData

clsFlags

clsStatistics
```

---

# Properties

## Metadata

```vb
Public Metadata As clsMetadata
```

Contains

DA

Width

GaugeLength

Future fields

---

## Raw Data

```vb
Public Raw As clsRawData
```

Contains

PointNo()

Time()

Crosshead()

Extensometer()

Force()

---

## Calculated Data

```vb
Public Calc As clsCalculatedData
```

Contains

Stress()

Strain()

TrueStress()

TrueStrain()

CorrectedStrain()

YoungModulus()

Yield()

Future arrays

---

## Flags

```vb
Public Flags As clsFlags
```

Contains

Imported

Validated

ExtensometerAvailable

FractureDetected

YieldDetected

GraphCorrected

---

## Statistics

```vb
Public Statistics As clsStatistics
```

Contains

PointCount

MaximumForce

MinimumForce

MaximumExtension

MaximumTime

---

# Methods

## Initialize

```vb
Dataset.Initialize
```

Creates internal objects.

---

## Allocate

```vb
Dataset.Allocate(PointCount)
```

Allocates every array.

---

## Clear

```vb
Dataset.Clear
```

Clears calculated values.

Raw data remain.

---

## Reset

```vb
Dataset.Reset
```

Deletes everything.

---

## Clone

```vb
NewDataset = Dataset.Clone
```

Creates deep copy.

---

## Validate

```vb
Dataset.Validate
```

Checks

Array Length

Metadata

Required Data

Returns

True

False

---

## Release

```vb
Dataset.Release
```

Releases memory.

---

# Memory Ownership

Import Engine

↓

Raw

Calculation Engine

↓

Calc

Graph Engine

↓

Read Only

Report Engine

↓

Read Only

---

# Access Example

```vb
Dim Dataset As New clsEngineeringDataset

Dataset.Metadata.GaugeLength

Dataset.Raw.Force(150)

Dataset.Calc.Stress(150)

Dataset.Flags.ExtensometerAvailable
```

---

# Advantages

No global variables

No worksheet dependency

Easy cloning

Undo support

Future .NET compatibility

Object encapsulation

Memory control

---

# Engineering Rule

Only this object is exchanged between Engines.

TXT File

↓

EngineeringDataset

↓

Everything Else

No Engine receives worksheet references.

---

# Lifetime

Import

↓

Initialize

↓

Allocate

↓

Fill

↓

Calculate

↓

Graph

↓

Report

↓

Archive

↓

Release

---

# Acceptance

✔ Object Based

✔ Array Based

✔ High Performance

✔ Encapsulated

✔ Excel Independent

✔ SQLite Compatible

✔ Future VB.NET Compatible

---

End Of Document
