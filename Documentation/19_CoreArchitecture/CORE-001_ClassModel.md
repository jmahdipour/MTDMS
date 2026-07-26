# MTDMS Complete Class Model

Document ID

MTDMS-CORE-001

Version

1.0

Status

Core Architecture

Platform

Excel 2019 VBA

Language

VBA

Application

MTDMS

---

# Purpose

This document defines every major class used inside MTDMS.

The objective is

High Cohesion

Low Coupling

High Performance

Easy Maintenance

Future VB.NET Compatibility

---

# Global Architecture

```

Application

│

├── Import Layer

├── Dataset Layer

├── Calculation Layer

├── Graph Layer

├── Report Layer

├── Archive Layer

└── UI Layer

```

---

# Import Layer

## clsTXTImporter

Responsibilities

Open TXT

Read Metadata

Read Curve

Build Dataset

---

## clsTXTParser

Responsibilities

Interpret Sections

Detect Format

Route Parsers

---

## clsMetadataParser

Read

d/a

b

L0

Future Metadata

---

## clsCurveParser

Read

No

Time

Displacement

Deformationt

Force

---

# Dataset Layer

## clsEngineeringDataset

Master Object

Contains

Metadata

Raw

Calc

Flags

Statistics

---

## clsMetadata

Contains

DA

Width

GaugeLength

Future Fields

---

## clsRawData

Contains

```
PointNo()

Time()

Crosshead()

Extensometer()

Force()
```

---

## clsCalculatedData

Contains

```
Stress()

Strain()

TrueStress()

TrueStrain()

CorrectedStrain()

YoungModulus()

Yield()

Rt()

Rp()

```

---

## clsStatistics

Contains

Maximum Force

Minimum Force

Point Count

Maximum Extension

Maximum Time

Sampling Interval

---

## clsFlags

Contains

Imported

Validated

FractureDetected

YieldDetected

ExtensometerAvailable

GraphCorrected

---

# Calculation Layer

## clsCalculationEngine

Coordinator

Calls

Stress

Strain

Young

Yield

etc.

---

## clsStressEngine

Only

Stress

---

## clsStrainEngine

Only

Strain

---

## clsYoungModulusEngine

Only

Young Modulus

---

## clsYieldEngine

Only

Rp

Rt

Upper Yield

Lower Yield

---

## clsFractureEngine

Detect Break

---

## clsCurveCorrectionEngine

Horizontal Correction

Elastic Region

Young Alignment

---

## clsSpringEngine

Spring Constant

---

## clsRingStiffnessEngine

Ring Stiffness

---

## clsBendingEngine

Three Point

Four Point

---

# Math Layer

## clsVectorMath

Vector Operations

---

## clsInterpolation

Interpolation

---

## clsFiltering

Moving Average

Median

Savitzky

Future

---

## clsStatisticsMath

Mean

Std

Variance

---

## clsSearch

Maximum

Minimum

Nearest

Peak

---

# Graph Layer

## clsGraphEngine

Create Graph

---

## clsGraphCorrection

Visual Correction

---

## clsGraphMarker

Yield

Fracture

Maximum

---

# Report Layer

## clsReportEngine

Main Report

---

## clsSummaryReport

INSO 3132

Mabhas 9

---

## clsReportExporter

PDF

Excel

CSV

---

# Archive Layer

## clsSQLite

SQLite Interface

---

## clsAudit

Audit Trail

---

## clsBackup

Backup Manager

---

# UI Layer

Ribbon

Settings

Dialogs

Progress

No Engineering Calculations

---

# Object Ownership

TXTImporter

↓

EngineeringDataset

↓

CalculationEngine

↓

GraphEngine

↓

ReportEngine

↓

SQLite

---

# Forbidden Dependencies

Graph

↓

Calculation

❌

Calculation

↓

Graph

❌

Report

↓

TXT

❌

SQLite

↓

Calculation

❌

Only

EngineeringDataset

connects Engines.

---

# Estimated Class Count

Import

4

Dataset

5

Calculation

9

Math

5

Graph

3

Report

3

Archive

3

UI

5

Total

≈37 Classes

---

# Acceptance

✔ Fully Modular

✔ Array Based

✔ Object Oriented

✔ Excel Independent

✔ Future Compatible

✔ High Performance

✔ ISO 17025 Ready

---

End Of Document
