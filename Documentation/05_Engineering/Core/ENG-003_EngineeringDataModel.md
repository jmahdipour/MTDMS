# Engineering Data Model

Document ID : MTDMS-ENG-003

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Application

MTDMS

Module

Engineering Core

---

# Purpose

This document defines the unified engineering data model used throughout MTDMS.

Every engineering module shall exchange data using this model.

No module shall directly access worksheet cells or raw TXT arrays.

---

# Design Philosophy

Raw Data

↓

Engineering Object

↓

Calculation Modules

↓

Graph Engine

↓

Report Engine

↓

SQLite

---

# Engineering Object

```
EngineeringResult
```

Contains every calculated property of one specimen.

One specimen

↓

One EngineeringResult

---

# Object Structure

```
EngineeringResult

├── Identification

├── Geometry

├── Material

├── Machine

├── Standard

├── Raw Data

├── Engineering Data

├── True Data

├── Yield

├── Strength

├── Fracture

├── Statistics

├── Validation

└── Metadata
```

---

# Identification

ProjectID

SessionID

SpecimenID

Operator

DateTime

ImportSession

---

# Machine Information

MachineID

MachineName

MachineModel

LoadCell

Extensometer

SoftwareVersion

---

# Material Information

MaterialName

MaterialGrade

MaterialLibraryID

YoungReference

YieldReference

UTSReference

---

# Standard Information

StandardID

StandardName

Revision

CalculationMethod

---

# Geometry

OriginalDiameter

OriginalWidth

OriginalThickness

OriginalArea

GaugeLength

FinalDiameter

FinalWidth

FinalThickness

FinalArea

---

# Raw Data

Arrays

Time()

Force()

Stroke()

Extension()

Temperature()

Speed()

---

# Engineering Data

Arrays

EngineeringStress()

EngineeringStrain()

---

# True Data

Arrays

TrueStress()

TrueStrain()

---

# Elastic Region

ElasticStartIndex

ElasticEndIndex

RegressionSlope

RegressionIntercept

RegressionR²

YoungMeasured

YoungCorrected

---

# Yield Data

YieldMethod

YieldIndex

YieldForce

YieldStress

YieldStrain

YieldExtension

---

# Ultimate Strength

MaximumForce

UltimateStress

UltimateIndex

---

# Fracture

FractureIndex

FractureForce

FractureStress

FractureExtension

FractureTime

---

# Ductility

ElongationPercent

ReductionOfAreaPercent

---

# Statistics

AverageStress

MaximumStress

MinimumStress

StandardDeviation

CoefficientOfVariation

---

# Validation

ValidationStatus

ValidationWarnings

ValidationErrors

OperatorApproval

---

# Metadata

ParserVersion

CalculationVersion

GraphVersion

ReportVersion

Checksum

AuditID

---

# VBA Class

Recommended

```
clsEngineeringResult
```

Every imported specimen

↓

Creates one class instance.

---

# SQLite Mapping

```
tblEngineeringResult
```

Stores summary values only.

Large arrays remain in

```
tblEngineeringData
```

---

# Graph Engine

Graph Engine receives

EngineeringResult

Only

Never reads

TXT

Never reads

SQLite

Directly.

---

# Report Engine

Receives

EngineeringResult

Generates

Certificate

PDF

Excel

CSV

---

# Memory Management

EngineeringResult

Created

↓

Used

↓

Saved

↓

Released

No object shall remain in memory after project closure.

---

# Future Expansion

Fatigue

Creep

Relaxation

Fracture Mechanics

Plasticity

Digital Image Correlation

Reserved

---

# Acceptance Criteria

✔ One unified engineering object

✔ Independent of TXT format

✔ Independent of worksheet structure

✔ Compatible with SQLite

✔ Compatible with Graph Engine

✔ Compatible with Report Engine

✔ Excel 2019 VBA compatible

---

End of Document
