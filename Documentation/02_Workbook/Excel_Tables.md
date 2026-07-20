# Excel Tables Specification

Document ID : MTDMS-WB-005

Version : 0.1.0

Platform

Microsoft Excel 2019

Workbook

WorkbookTemplate.xlsm

---

# Purpose

This document defines every Excel Table (ListObject) used in the workbook.

All structured data shall be stored inside Excel Tables.

Normal cell ranges are prohibited for engineering data.

---

# Naming Convention

Every table shall start with

```
tbl
```

Example

```
tblRawData
```

---

# HOME

## tblRecentProjects

Purpose

Recent Projects

Columns

ProjectID

ProjectName

Material

Standard

Operator

Date

Status

---

# IMPORT

## tblTXTPreview

Purpose

TXT Preview

Columns

Row

Column1

Column2

...

Dynamic

---

## tblValidation

Purpose

Validation Results

Columns

Rule

Status

Description

---

# RAW_DATA

## tblRawData

Purpose

Stores imported TXT exactly as received.

Columns

Index

Time

Stroke

Extension

Force

Stress

Strain

Engineering calculations

NO

---

# ENGINEERING

## tblEngineering

Purpose

Intermediate engineering calculations.

Columns

Index

EngineeringStress

EngineeringStrain

TrueStress

TrueStrain

ElasticCorrection

YoungRegion

YieldRegion

Regression

---

# RESULT

## tblResult

Purpose

Validated engineering results.

Columns

Property

Value

Unit

Tolerance

Status

Example

Young's Modulus

Yield Strength

UTS

Elongation

Reduction of Area

Maximum Load

Fracture Load

---

# MATERIAL_DB

## tblMaterial

Columns

MaterialID

MaterialName

Young

Yield

UTS

Density

Poisson

ThermalExpansion

Reference

Revision

---

# STANDARD_DB

## tblStandard

Columns

StandardID

StandardName

Revision

CalculationMethod

Reference

Status

---

# SETTINGS

## tblSettings

Columns

Parameter

Value

Description

---

# HISTORY

## tblHistory

Columns

ProjectID

Date

Operator

Machine

Material

Result

ReportNumber

---

# ERROR_LOG

## tblErrorLog

Columns

Timestamp

Module

Procedure

ErrorCode

Description

Severity

Resolved

---

# SYSTEM

## tblSystem

Columns

Variable

Value

LastModified

---

# Table Style

Style

TableStyleMedium2

Header

Dark Blue

Banding

Enabled

Filter

Enabled

Totals Row

Disabled

---

# Sorting

All engineering tables

Ascending by Index

History

Descending by Date

Material Library

Ascending by Material Name

---

# Filtering

Enabled

Except

ENGINEERING

SYSTEM

---

# Design Rules

✔ Every dataset shall be stored in a ListObject.

✔ VBA shall access tables by name.

Correct

```vb
Set lo = Worksheets("RAW_DATA").ListObjects("tblRawData")
```

Wrong

```vb
Range("A1:F50000")
```

---

# Future Tables

tblCompression

tblImpact

tblFatigue

tblCalibration

tblSPC

---

End of Document
