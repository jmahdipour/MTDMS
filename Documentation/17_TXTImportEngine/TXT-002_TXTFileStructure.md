# TXT File Structure Specification

Document ID : MTDMS-TXT-002

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Primary Data Source

TXT File (Testing Machine Export)

Application

MTDMS

Status

Production

---

# Purpose

This document defines the canonical structure of the TXT files imported into MTDMS.

The objective is to provide a machine-independent internal model capable of importing TXT files from different generations of testing software without modifying the Engineering Calculation Engine.

The TXT Import Engine converts every supported TXT file into a common Engineering Dataset.

No engineering calculations are performed in this stage.

---

# Design Philosophy

The internal software architecture shall never depend directly on the exact layout of one manufacturer's TXT file.

Instead

Machine TXT

↓

Import Layer

↓

Normalized Engineering Dataset

↓

Calculation Engine

↓

Graph Engine

↓

Report Engine

This separation allows future support for new machine models without changing engineering algorithms.

---

# Logical Sections

Every imported TXT file is interpreted as a collection of logical sections.

Typical sections

```
Header

Machine Information

Software Information

Operator Information

Customer Information

Project Information

Sample Information

Material Information

Test Parameters

Load Cell Information

Extensometer Information

Channel Definitions

Curve Data

Calculated Values (optional)

Footer
```

Actual physical order may differ.

---

# Required Sections

Minimum required

Header

Machine

Sample

Curve Data

Without these sections the file cannot be imported.

---

# Optional Sections

Customer

Project

Material

Calculated Results

Comments

Environmental Conditions

These are imported whenever available.

---

# Header Section

The Header normally contains

Software Name

Software Version

Machine Name

Export Date

Export Time

Language

Separator

Encoding

Import Timestamp

---

# Machine Information

Typical fields

Machine Model

Machine Serial Number

Capacity

Frame Type

Crosshead Type

Drive Type

Controller

PLC

Software Version

Calibration Date

Administrator configurable.

---

# Operator Information

Typical fields

Operator Name

Operator ID

Department

Shift

Supervisor

Optional.

---

# Customer Information

Typical fields

Customer Name

Customer Code

Purchase Order

Project

Drawing Number

Optional.

---

# Sample Information

Typical fields

Sample ID

Material

Material Grade

Heat Number

Batch Number

Specimen Number

Orientation

Dimensions

Gauge Length

Width

Thickness

Diameter

Cross Section

These values become part of the Engineering Dataset.

---

# Test Parameters

Typical fields

Test Standard

Control Mode

Speed

Preload

Sampling Rate

Stop Condition

Maximum Stroke

Maximum Force

Optional Parameters

---

# Load Cell Section

Typical fields

Load Cell ID

Capacity

Unit

Calibration Date

Calibration Status

Serial Number

Administrator configurable.

---

# Extensometer Section

Typical fields

Extensometer ID

Gauge Length

Measurement Range

Resolution

Calibration Date

Optional.

---

# Channel Definition Section

Each recorded channel shall contain

Channel Name

Physical Quantity

Unit

Column Number

Scaling Information

Examples

Force

Extension

Crosshead Position

Time

Strain

Stress

Temperature

Administrator configurable.

---

# Curve Data Section

The Curve Data section contains sequential measurement points.

Typical structure

```
Point

Time

Force

Extension

Crosshead

Optional Channels
```

The Import Engine stores raw values only.

---

# Calculated Values Section

Some machine software exports calculated values.

Examples

Yield

UTS

Modulus

Elongation

Reduction of Area

These values are imported as reference only.

The Engineering Calculation Engine shall never trust these values without recalculation.

---

# Footer

Typical footer

Export Finished

Checksum

Comments

End Of File Marker

Optional.

---

# Normalized Engineering Dataset

Regardless of the original TXT layout

every imported file shall generate one standardized Engineering Dataset.

Dataset includes

Machine

Operator

Customer

Sample

Material

Test Parameters

Load Cell

Extensometer

Curve Data

Metadata

No calculated engineering properties.

---

# Section Independence

Each parser operates independently.

Example

Header

↓

Machine

↓

Sample

↓

Curve

Failure in one section shall not necessarily stop the import unless that section is mandatory.

---

# Future Compatibility

The structure supports future import of

CSV

XML

JSON

Binary Export

Direct Database Export

without changing downstream engines.

---

# Engineering Independence

This document defines data organization only.

It does not define

Yield calculations

Stress calculations

Young's Modulus

Elongation

Graph generation

Reporting

---

# SQLite Interaction

Optional metadata stored

File Name

Machine

Operator

Import Date

Software Version

TXT Format Version

Import Status

Engineering data are passed to the Engineering Dataset.

---

# Acceptance Criteria

✔ Supports multiple TXT layouts

✔ Machine-independent architecture

✔ Mandatory section validation

✔ Optional section support

✔ Future format compatibility

✔ Excel 2019 compatible

✔ SQLite compatible

✔ No engineering calculations

✔ Complete traceability to original TXT file

---

# Related Documents

TXT-001_Architecture

TXT-003_VersionDetection

TXT-004_FileEncoding

TXT-005_ParserEngine

TXT-016_EngineeringDatasetBuilder

---

End of Document
