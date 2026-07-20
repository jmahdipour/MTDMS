# 05_Engineering

Document ID : MTDMS-ENG-001

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

---

# Purpose

The Engineering Module performs all engineering calculations required after successful TXT import.

The module converts validated raw data into engineering results according to applicable international standards.

No calculation shall use raw imported values directly without passing through the Engineering Pipeline.

---

# Responsibilities

The Engineering Module is responsible for

• Engineering Stress

• Engineering Strain

• True Stress

• True Strain

• Young's Modulus

• Elastic Region Detection

• Yield Point Detection

• Rp Calculations

• Rt Calculations

• Tensile Strength

• Fracture Detection

• Elongation

• Reduction of Area

• Bending Calculations

• Compression Calculations

• Spring Calculations

• Ring Stiffness

• Charpy

• Hardness

• Statistical Analysis

• Measurement Uncertainty

---

# Input

Validated Raw Data

↓

Engineering Engine

↓

Results

---

# Output

Engineering Dataset

↓

Graphs

↓

Reports

↓

Database

---

# Standards

ISO 6892-1

ASTM E8/E8M

ASTM E111

ISO 7500-1

ISO 6805

INSO 3132

ISO 630

ISO 898

---

# Architecture

Engineering calculations are divided into independent modules.

Every module receives

Validated Engineering Input

and returns

Validated Engineering Output.

No module modifies imported raw data.

---

# Development Status

Module

In Development
