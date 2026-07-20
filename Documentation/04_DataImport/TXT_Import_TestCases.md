# TXT Import Test Cases

Document ID : MTDMS-IMP-046

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Import Engine

---

# Purpose

This document defines all functional test cases required to verify the TXT Import Engine.

Every software release shall pass these tests before deployment.

These tests validate

• Parser

• Import

• SQLite

• Engineering initialization

• Ribbon behavior

• Audit Trail

---

# Test Categories

1

File Tests

2

Header Tests

3

Column Tests

4

Unit Tests

5

Material Tests

6

Standard Tests

7

Geometry Tests

8

SQLite Tests

9

Engineering Tests

10

Performance Tests

11

Recovery Tests

---

# FILE TESTS

## TC-001

Description

Import valid TXT

Expected

PASS

Project Created

Raw Data Stored

Engineering Ready

---

## TC-002

TXT does not exist

Expected

Error

IMP-0001

---

## TC-003

Empty TXT

Expected

Import aborted

---

## TC-004

Wrong Extension

Example

CSV

Expected

Rejected

---

## HEADER TESTS

## TC-010

Missing Material

Expected

Material Selection Dialog

---

## TC-011

Missing Standard

Expected

Standard Selection Dialog

---

## TC-012

Missing Machine

Expected

Machine Profile Selection

---

## COLUMN TESTS

## TC-020

Missing Force Column

Expected

Critical Error

---

## TC-021

Missing Time Column

Expected

Critical Error

---

## TC-022

Unknown Extra Column

Expected

Ignored

Logged

Import Continues

---

## UNIT TESTS

## TC-030

Force in kN

Expected

Converted to Newton

---

## TC-031

Force in kgf

Expected

Converted

---

## TC-032

Length in inch

Expected

Converted to mm

---

## MATERIAL TESTS

## TC-040

Known Material

Expected

Automatic Match

---

## TC-041

Alias Material

Expected

Alias Accepted

Warning Logged

---

## TC-042

Unknown Material

Expected

Manual Selection

---

## STANDARD TESTS

## TC-050

ISO6892

Expected

ISO6892-1 Loaded

---

## TC-051

ASTM E8M

Expected

ASTM E8 Profile Loaded

---

## GEOMETRY TESTS

## TC-060

Round Specimen

Expected

Area Calculated

---

## TC-061

Flat Specimen

Expected

Area Calculated

---

## TC-062

Pipe

Expected

Pipe Formula Used

---

## SQLITE TESTS

## TC-070

New Project

Expected

Records Created

---

## TC-071

Duplicate TXT

Expected

Duplicate Warning

---

## TC-072

Database Locked

Expected

Rollback

---

## ENGINEERING TESTS

## TC-080

Engineering Stress

Expected

Calculated

---

## TC-081

Engineering Strain

Expected

Calculated

---

## TC-082

True Stress

Expected

Calculated

---

## TC-083

True Strain

Expected

Calculated

---

## PERFORMANCE TESTS

## TC-090

1000 Samples

Target

<1 Second

---

## TC-091

10000 Samples

Target

<2 Seconds

---

## TC-092

100000 Samples

Target

<10 Seconds

---

## RECOVERY TESTS

## TC-100

Import Cancelled

Expected

Rollback

---

## TC-101

Power Failure Simulation

Expected

SQLite Consistent

---

## TC-102

Unexpected VBA Error

Expected

Workbook Remains Stable

---

# Ribbon Tests

## TC-110

Before Import

Engineering Buttons Disabled

---

## TC-111

After Import

Engineering Buttons Enabled

---

## TC-112

Error State

Retry Enabled

---

# Graph Tests

## TC-120

Graph Created

Expected

PASS

---

## TC-121

Yield Marker

Displayed

---

## TC-122

Fracture Marker

Displayed

---

# Audit Tests

## TC-130

Import Logged

Expected

PASS

---

## TC-131

Operator Override Logged

PASS

---

## TC-132

Warning Logged

PASS

---

# Acceptance Criteria

100%

Critical Tests

PASS

95%

Overall Tests

PASS

0

Database Corruption

Allowed

0

Workbook Crash

Allowed

---

# Regression Tests

Every software update

Must execute

All Test Cases

Before Release.

---

End of Document
