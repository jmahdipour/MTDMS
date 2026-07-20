# TXT Header Alias Dictionary

Document ID : MTDMS-IMP-038

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Application

MTDMS

---

# Purpose

This document defines every supported header alias that may appear inside TXT files.

Different manufacturers use different names for the same engineering parameter.

The parser shall convert all aliases into one internal standard name.

The Engineering Engine shall never use external names.

---

# Architecture

TXT Header

↓

Alias Dictionary

↓

Internal Header

↓

Engineering Engine

---

# Storage

SQLite

Table

tblHeaderAlias

---

# Table Structure

| Alias | Internal Name | Required |
|---------|---------------|----------|
| Force | Force | Yes |
| Load | Force | Yes |
| Test Force | Force | Yes |

---

# Header Groups

Headers are classified into

Machine

Project

Material

Specimen

Geometry

Engineering

Administrative

Reserved

---

# Machine Headers

| Accepted Header | Internal Name |
|-----------------|---------------|
| Machine | MachineName |
| Tester | MachineName |
| Testing Machine | MachineName |
| Equipment | MachineName |
| Device | MachineName |

---

# Machine Model

| Alias | Internal |
|---------|----------|
| Model | MachineModel |
| Machine Model | MachineModel |
| Equipment Model | MachineModel |

---

# Serial Number

| Alias | Internal |
|---------|----------|
| Serial | MachineSerial |
| Serial No | MachineSerial |
| Serial Number | MachineSerial |
| SN | MachineSerial |

---

# Material Headers

| Alias | Internal |
|---------|----------|
| Material | Material |
| Grade | Material |
| Steel Grade | Material |
| Alloy | Material |
| Material Name | Material |

---

# Standard Headers

| Alias | Internal |
|---------|----------|
| Standard | Standard |
| Test Standard | Standard |
| ISO | Standard |
| ASTM | Standard |
| DIN | Standard |
| EN | Standard |
| INSO | Standard |

---

# Project Headers

| Alias | Internal |
|---------|----------|
| Project | ProjectName |
| Job | ProjectName |
| Work Order | ProjectName |
| Order | ProjectName |

---

# Operator Headers

| Alias | Internal |
|---------|----------|
| Operator | Operator |
| User | Operator |
| Technician | Operator |
| Inspector | Operator |

---

# Specimen Headers

| Alias | Internal |
|---------|----------|
| Specimen | SpecimenID |
| Sample | SpecimenID |
| Test Piece | SpecimenID |
| Coupon | SpecimenID |

---

# Area Headers

| Alias | Internal |
|---------|----------|
| Area | Area |
| Cross Section | Area |
| Cross-sectional Area | Area |
| Section Area | Area |

---

# Gauge Length

| Alias | Internal |
|---------|----------|
| L0 | GaugeLength |
| Gauge Length | GaugeLength |
| Initial Length | GaugeLength |
| Original Length | GaugeLength |

---

# Diameter

| Alias | Internal |
|---------|----------|
| Diameter | Diameter |
| Dia | Diameter |
| d | Diameter |
| Ø | Diameter |
| Outside Diameter | Diameter |

---

# Width

| Alias | Internal |
|---------|----------|
| Width | Width |
| b | Width |
| Specimen Width | Width |

---

# Thickness

| Alias | Internal |
|---------|----------|
| Thickness | Thickness |
| t | Thickness |
| Wall Thickness | Thickness |

---

# Pipe Headers

| Alias | Internal |
|---------|----------|
| OD | OutsideDiameter |
| Do | OutsideDiameter |
| Outside Diameter | OutsideDiameter |
| Pipe Diameter | OutsideDiameter |

---

# Time Headers

| Alias | Internal |
|---------|----------|
| Time | Time |
| Test Time | Time |
| Seconds | Time |
| Elapsed Time | Time |

---

# Force Headers

| Alias | Internal |
|---------|----------|
| Force | Force |
| Load | Force |
| Applied Force | Force |
| Test Force | Force |
| Load Cell | Force |

---

# Stroke Headers

| Alias | Internal |
|---------|----------|
| Stroke | Stroke |
| Crosshead | Stroke |
| Crosshead Position | Stroke |
| Displacement | Stroke |
| Travel | Stroke |

---

# Extension Headers

| Alias | Internal |
|---------|----------|
| Extension | Extension |
| Elongation | Extension |
| Gauge Extension | Extension |
| Extensometer | Extension |

---

# Stress Headers

| Alias | Internal |
|---------|----------|
| Stress | Stress |
| Engineering Stress | Stress |
| Sigma | Stress |

---

# Strain Headers

| Alias | Internal |
|---------|----------|
| Strain | Strain |
| Engineering Strain | Strain |
| Epsilon | Strain |

---

# Temperature

| Alias | Internal |
|---------|----------|
| Temperature | Temperature |
| Temp | Temperature |
| °C | Temperature |

---

# Speed

| Alias | Internal |
|---------|----------|
| Speed | Speed |
| Test Speed | Speed |
| Crosshead Speed | Speed |

---

# Unknown Headers

Unknown headers

↓

Ignored

↓

Logged

↓

Stored in Import Log

They shall never stop the import process.

---

# Administrator

Administrator may

Add Alias

Disable Alias

Edit Alias

Export Alias Dictionary

Import Alias Dictionary

No VBA modification required.

---

# Acceptance Criteria

✔ Unlimited aliases

✔ SQLite configurable

✔ Case insensitive

✔ Unicode supported

✔ Machine independent

✔ Excel 2019 compatible

---

End of Document
