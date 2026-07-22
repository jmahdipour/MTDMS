# Calculation Profile Database

Document ID : MTDMS-DB-029

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Application

MTDMS

Status

Production

---

# Purpose

The Calculation Profile Database defines which engineering calculations are available for each test type.

A Calculation Profile is a configuration object.

It specifies **what calculations shall be performed**, **which parameters are required**, and **which outputs are expected**.

It does not contain formulas.

It does not perform calculations.

---

# Objectives

The Calculation Profile Database shall

• Define calculation workflows

• Associate calculations with standards

• Control required inputs

• Define expected outputs

• Support future test types

---

# Design Philosophy

TXT File

↓

Import

↓

Calculation Profile

↓

Calculation Engine

↓

Engineering Results

The profile controls the calculation workflow.

The Calculation Engine performs the mathematics.

---

# Table Name

tblCalculationProfile

---

# Primary Key

CalculationProfileID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

CalculationProfileID

INTEGER

----------------------------

ProfileCode

TEXT

Unique

Examples

ISO6892

ASTME8

SPRING_K

RING_STIFFNESS

BENDING_3P

BENDING_4P

CUSTOM

----------------------------

ProfileName

TEXT

----------------------------

StandardID

INTEGER

Nullable

Foreign Key

tblStandard

----------------------------

TestCategory

TEXT

Examples

Tensile

Compression

Bending

Spring

Ring Stiffness

Impact

Hardness

Plastic

Custom

----------------------------

CalculationSequence

INTEGER

Execution order

----------------------------

RequiresMaterialLibrary

BOOLEAN

----------------------------

RequiresYoungModulus

BOOLEAN

----------------------------

RequiresGeometry

BOOLEAN

----------------------------

RequiresManualInput

BOOLEAN

----------------------------

SupportsGraphCorrection

BOOLEAN

----------------------------

SupportsAutomaticYieldDetection

BOOLEAN

----------------------------

SupportsManualYieldCorrection

BOOLEAN

----------------------------

SupportsCSVExport

BOOLEAN

----------------------------

SupportsReportGeneration

BOOLEAN

----------------------------

SupportsCertificateGeneration

BOOLEAN

----------------------------

Active

BOOLEAN

----------------------------

Remarks

TEXT

Nullable

----------------------------

CreatedDate

DATE

----------------------------

ModifiedDate

DATE

----------------------------

ModifiedBy

TEXT

---

# Typical Profiles

ISO 6892-1 Tensile

ASTM E8 Tensile

Compression

Three Point Bending

Four Point Bending

Spring Constant

Ring Stiffness

Plastic Tensile

Administrator configurable.

---

# Required Inputs

Each profile may require

TXT Data

Material Library

Geometry

Manual Dimensions

Operator Confirmation

Secondary Gauge Length

Reference Standard

---

# Expected Outputs

Yield Strength

Ultimate Strength

Young's Modulus

Maximum Force

Maximum Displacement

Elongation

Reduction of Area

Spring Constant

Ring Stiffness

Energy

Custom Outputs

---

# Engineering Independence

Profiles

define

workflow only.

Profiles never contain

equations

constants

engineering results.

---

# SQLite Relationships

tblCalculationProfile

↓

N : 1

tblStandard

↓

Referenced by

Calculation Engine

Validation Engine

Report Engine

---

# Indexes

IX_ProfileCode

IX_TestCategory

IX_StandardID

---

# Constraints

ProfileCode

UNIQUE

TestCategory

Required

---

# Audit Trail

Store

Profile

Modification

Operator

Timestamp

Computer

Software Version

---

# Permissions

Administrator

Modify

Quality Manager

Modify

Reviewer

Read

Operator

Read Only

---

# Error Handling

Missing Profile

↓

Abort Calculation

Inactive Profile

↓

Reject

Unknown Test Category

↓

Reject

Duplicate Profile Code

↓

Reject

---

# Acceptance Criteria

✔ Multiple calculation profiles supported

✔ Standard linkage supported

✔ Workflow configuration only

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations performed separately

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
