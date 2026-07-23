# Engineering Formula Library

Document ID : MTDMS-CE-020

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Primary Data Source

TXT File

Application

MTDMS

Status

Production

---

# Purpose

The Engineering Formula Library defines every engineering equation, mathematical relationship, and calculation dependency used throughout MTDMS.

It serves as the authoritative reference for all engineering modules.

The Formula Library itself performs **no calculations**.

It documents the mathematical models used by the Calculation Engine.

---

# Objectives

The Formula Library shall

• Centralize engineering formulas

• Standardize calculations

• Support multiple standards

• Maintain engineering consistency

• Provide complete traceability

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Formula Library

↓

Calculation Engine

↓

Engineering Results

All engineering modules use formulas defined here.

---

# Formula Categories

Geometry

Stress

Strain

Elasticity

Yield

True Stress

True Strain

Compression

Bending

Spring

Ring Stiffness

Statistics

Future Modules

---

# Geometry

## Round Specimen Area

\[
A=\frac{\pi d^2}{4}
\]

---

## Flat Specimen Area

\[
A=bt
\]

---

## Pipe Area

\[
A=\frac{\pi}{4}(D^2-d^2)
\]

---

# Tensile Test

## Engineering Stress

\[
\sigma=\frac{F}{A_0}
\]

---

## Engineering Strain

\[
\varepsilon=\frac{\Delta L}{L_0}
\]

---

## True Stress

\[
\sigma_t=\sigma(1+\varepsilon)
\]

(before necking)

---

## True Strain

\[
\varepsilon_t=\ln(1+\varepsilon)
\]

---

# Elasticity

## Young's Modulus

\[
E=\frac{\Delta\sigma}{\Delta\varepsilon}
\]

---

# Compression

## Compressive Stress

\[
\sigma_c=\frac{F}{A_0}
\]

---

## Compressive Strain

\[
\varepsilon_c=\frac{\Delta L}{L_0}
\]

Sign convention is defined by the selected calculation profile.

---

# Three-Point Bending

## Flexural Stress

\[
\sigma_f=\frac{3FL}{2bh^2}
\]

---

## Flexural Strain

\[
\varepsilon_f=\frac{6Dh}{L^2}
\]

---

# Four-Point Bending

The exact equations depend on

Selected Standard

Loading Configuration

Calculation Profile

No formula shall be hardcoded outside the calculation profile.

---

# Spring

## Spring Constant

\[
K=\frac{\Delta F}{\Delta x}
\]

---

# Ring Stiffness

Ring stiffness equations are obtained from

Selected Standard

Calculation Profile

No hardcoded implementation is permitted.

---

# Statistics

## Arithmetic Mean

\[
\bar{x}=\frac{1}{n}\sum x_i
\]

---

## Standard Deviation

Sample

\[
s=\sqrt{\frac{\sum(x_i-\bar{x})^2}{n-1}}
\]

---

## Coefficient of Variation

\[
CV=\frac{s}{\bar{x}}\times100
\]

---

# Formula Management

Each formula shall include

Name

Description

Variables

Engineering Units

Applicable Standards

Calculation Profile

Revision History

---

# Engineering Independence

The Formula Library

contains only

engineering definitions.

It never

imports TXT

stores results

modifies reports

communicates with SQLite

It serves as the mathematical reference.

---

# SQLite Interaction

SQLite stores

Formula Metadata

Formula Revision

Calculation Profile Mapping

No engineering calculations are executed inside SQLite.

---

# Acceptance Criteria

✔ Geometry formulas documented

✔ Tensile formulas documented

✔ Compression formulas documented

✔ Bending formulas documented

✔ Spring formulas documented

✔ Statistical formulas documented

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Mathematical traceability complete

---

# End of Calculation Engine Chapter
