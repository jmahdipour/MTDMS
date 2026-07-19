# Requirements Specification

Document ID: MTDMS-SRS-001

Version: 0.1.0

Status: Draft

---

# 1. Purpose

This document defines the functional and non-functional requirements of the Mechanical Testing Data Management System (MTDMS).

The requirements described here are mandatory for software implementation.

---

# 2. Target Platform

Operating System

Microsoft Windows 10

Microsoft Windows 11

Office Version

Microsoft Excel 2019 (64-bit preferred)

Programming Language

Visual Basic for Applications (VBA)

Ribbon

Ribbon XML

Database

SQLite

Input Format

TXT Only

---

# 3. Functional Requirements

## FR-001

The software shall import TXT files exported from mechanical testing machines.

Priority

Critical

---

## FR-002

The software shall validate TXT file structure before import.

Validation includes

• Header

• Column count

• Numeric values

• Empty values

• Invalid characters

Priority

Critical

---

## FR-003

The software shall support Material Library.

Stored information

Material Name

Young's Modulus

Yield Strength

Ultimate Strength

Density

Poisson Ratio

Reference Standard

Priority

High

---

## FR-004

The software shall support Standard Library.

Examples

ISO 6892-1

ISO 7500-1

ISO 17025

ISO 630

ISO 898

INSO 3132

Priority

High

---

## FR-005

The software shall calculate engineering stress.

Priority

Critical

---

## FR-006

The software shall calculate engineering strain.

Priority

Critical

---

## FR-007

The software shall calculate true stress.

Priority

High

---

## FR-008

The software shall calculate true strain.

Priority

High

---

## FR-009

The software shall calculate Young's Modulus.

Priority

Critical

---

## FR-010

The software shall determine Yield Strength.

Supported

Upper Yield

Lower Yield

Rp0.2

Rp0.1

Manual Yield

Priority

Critical

---

## FR-011

The software shall determine Ultimate Tensile Strength.

Priority

Critical

---

## FR-012

The software shall determine fracture point.

Priority

Critical

---

## FR-013

The software shall calculate elongation after fracture.

Priority

Critical

---

## FR-014

The software shall calculate reduction of area.

Priority

High

---

## FR-015

The software shall display engineering graph.

Supported

Stress–Strain

Force–Stroke

Load–Deflection

Priority

Critical

---

## FR-016

Graph shall support

Zoom

Pan

Crosshair

Manual Marker

Undo

Reset

Priority

High

---

## FR-017

The software shall allow manual correction of Yield Point.

Priority

Critical

---

## FR-018

The software shall allow manual correction of Fracture Point.

Priority

High

---

## FR-019

The software shall generate PDF reports.

Priority

Critical

---

## FR-020

The software shall generate Excel reports.

Priority

High

---

## FR-021

The software shall store projects in SQLite.

Priority

Critical

---

## FR-022

The software shall maintain project history.

Priority

Medium

---

## FR-023

The software shall automatically save project settings.

Priority

Medium

---

## FR-024

The software shall support Ribbon interface only.

UserForms are prohibited.

Priority

Critical

---

## FR-025

The software shall maintain complete audit history.

Priority

Medium

---

# 4. Non-Functional Requirements

---

## NFR-001

Excel 2019 compatible.

---

## NFR-002

No external installation required.

---

## NFR-003

Offline operation.

---

## NFR-004

No internet dependency.

---

## NFR-005

Maximum TXT import time

Less than 5 seconds

(100000 rows)

---

## NFR-006

Automatic backup.

---

## NFR-007

Readable source code.

---

## NFR-008

Modular architecture.

---

## NFR-009

Maintainability.

---

## NFR-010

ISO/IEC 17025 compatible documentation.

---

# 5. Constraints

Only VBA

Only Ribbon XML

Only TXT

Only SQLite

Only Excel 2019

No UserForms

No ActiveX

No PLC Control

No Machine Motion

---

# 6. Acceptance Criteria

The software is considered acceptable when

✓ TXT file imports successfully

✓ Validation completes without errors

✓ Engineering calculations match reference values

✓ Graph is generated correctly

✓ Report is generated successfully

✓ SQLite database stores project correctly

✓ Ribbon operates without runtime errors

---

End of Document
