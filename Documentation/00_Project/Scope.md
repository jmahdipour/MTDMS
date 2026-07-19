# Scope

Version: 0.1.0

Status: Draft

---

# Purpose

This document defines the functional scope of MTDMS.

It clearly specifies what the software SHALL do and what it SHALL NOT do.

---

# Project Scope

MTDMS is an Engineering Data Management System developed entirely in

- Microsoft Excel 2019
- VBA
- Ribbon XML

Its purpose is to process mechanical testing data exported as TXT files.

---

# Supported Input

The software SHALL import

TXT files only.

Supported source

Universal Testing Machines

---

Unsupported

CSV

Excel

XML

PDF

Database Import

PLC Online Data

Machine Live Stream

---

# Supported Mechanical Tests

## Tensile Test

Supported

Engineering Stress

Engineering Strain

True Stress

True Strain

Young's Modulus

Upper Yield

Lower Yield

Rp0.2

Rp0.1

Maximum Load

Ultimate Tensile Strength

Fracture Load

Elongation

Reduction of Area

Elastic Region Correction

Graph Correction

Manual Yield Selection

Manual Fracture Selection

Noise Filtering

Automatic Validation

---

## Bend Test

3 Point

4 Point

Maximum Load

Stress

Deflection

---

## Shear Test

Maximum Shear Load

Shear Stress

Shear Displacement

---

## Spring Test

Spring Constant

Load

Deflection

Regression

---

## Ring Stiffness Test

Pipe Ring Stiffness

Load

Displacement

Instantaneous Stiffness

---

# Material Library

The software SHALL include

Steel

Stainless Steel

Cast Iron

Copper

Brass

Bronze

Aluminium

Zinc

Zamak

User Defined Materials

---

Stored Properties

Young's Modulus

Yield Strength

Ultimate Strength

Density

Poisson Ratio

Thermal Expansion

Reference Standard

---

# Standard Library

Supported

ISO 6892-1

ISO 7500-1

ISO 17025

ISO 630

ISO 898

INSO 3132

Expandable

ASTM

DIN

EN

BS

---

# Graph Engine

Supported

Stress-Strain

Force-Stroke

Load-Deflection

Zoom

Pan

Crosshair

Manual Marker

Automatic Marker

Graph Correction

Export

---

# Reports

Supported

Laboratory Report

Engineering Report

Summary Report

PDF

Excel

Print

---

# Database

SQLite

Projects

Materials

Standards

History

Results

Settings

Users

---

# Ribbon Interface

Supported

Home

Import

Calculation

Graph

Report

Database

Settings

Help

---

# Security

Read Only Libraries

Project Backup

History Logging

Error Logging

---

# Logging

Import Log

Calculation Log

Error Log

User Activity

---

# NOT Included

Machine Motion Control

PLC Programming

Servo Drive Control

Real-Time Acquisition

DAQ Hardware

Cloud Synchronization

Web Application

Mobile Application

Artificial Intelligence Decision Making

---

# Future Scope

Compression Test

Fatigue Test

Impact Test

Hardness Management

Calibration Management

SPC

Control Charts

Laboratory Dashboard

Multi-Language

Network Database

Automatic Backup

Digital Signature

---

# Scope Boundary

The software starts

TXT Import

↓

Engineering Processing

↓

Engineering Report

↓

Database Storage

The software ends after the engineering report is generated.

No interaction with the testing machine itself is included.

---

End of Document
