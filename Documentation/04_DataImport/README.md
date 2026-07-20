# 04_DataImport

Document ID : MTDMS-IMP-048

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Project

MTDMS

---

# Purpose

This folder contains all documents related to the TXT Import Engine.

The Import Engine is responsible for transforming machine-generated TXT files into validated engineering data that can be used by the remaining MTDMS modules.

This module is the entry point of the entire software.

No engineering calculations begin before the Import Engine successfully completes.

---

# Scope

The Import Engine is responsible for

✔ Reading TXT files

✔ Detecting machine type

✔ Recognizing material

✔ Recognizing standard

✔ Recognizing specimen geometry

✔ Detecting units

✔ Converting units

✔ Validating imported data

✔ Storing raw data

✔ Initializing engineering calculations

✔ Preparing graph data

✔ Creating audit records

---

# High-Level Architecture

```
TXT File

↓

Parser

↓

Validation

↓

Machine Recognition

↓

Material Recognition

↓

Standard Recognition

↓

Unit Conversion

↓

SQLite Storage

↓

Engineering Engine

↓

Graph Engine

↓

Report Engine
```

---

# Folder Contents

## Parser

TXT_Parser_Architecture.md

TXT_Parser_Modules.md

---

## File Format

TXT_File_Format.md

TXT_Header_Specification.md

TXT_HeaderAliasDictionary.md

TXT_ColumnAliasDictionary.md

TXT_Data_Columns.md

TXT_Compatibility.md

TXT_Examples.md

---

## Machine Recognition

TXT_Machine_Profiles.md

TXT_Machine_Profile_Generic.md

TXT_Machine_Profile_Shimadzu.md

TXT_Machine_Profile_FATEK.md

TXT_Machine_Profile_Configuration.md

---

## Material & Standards

TXT_Material_Library_Integration.md

TXT_Standard_Library_Integration.md

TXT_Specimen_Recognition.md

TXT_Test_Type_Detection.md

TXT_Dimension_Validation.md

---

## Units

TXT_Unit_Detection.md

TXT_UnitConversionEngine.md

---

## Validation

TXT_Validation.md

TXT_Error_Handling.md

TXT_Error_Codes.md

TXT_Warning_Handling.md

---

## Database

TXT_Raw_Data_Table.md

TXT_Raw_Data_Storage.md

TXT_SQLiteSynchronization.md

TXT_Project_Association.md

TXT_Checksum.md

TXT_Import_Audit_Trail.md

---

## Workflow

TXT_Import_Workflow.md

TXT_Import_Sequence.md

TXT_Import_StateMachine.md

TXT_Import_Settings.md

TXT_ImportWizard.md

TXT_Import_API.md

TXT_BatchImport.md

TXT_Import_TestCases.md

---

## Engineering Preparation

TXT_Engineering_Data_Generation.md

TXT_Graph_Data_Preparation.md

TXT_Graph_Correction_Preparation.md

TXT_Graph_Correction_Algorithm.md

---

## Miscellaneous

TXT_Import_Performance.md

TXT_Import_Security.md

---

# Dependencies

Import Engine

↓

Engineering Module

↓

Graph Module

↓

Reporting Module

No downstream module shall access TXT files directly.

All modules shall use validated engineering data only.

---

# External Standards

ISO/IEC 17025

ISO 6892-1

ISO 7500-1

ISO 6805

ASTM E8/E8M

ASTM E111

INSO 3132

ISO 630

ISO 898

---

# Database Dependency

SQLite is mandatory.

The Import Engine creates and updates

Projects

Import Sessions

Raw Data

Audit Trail

No Engineering calculations are permanently stored until import has completed successfully.

---

# Error Philosophy

Errors

↓

Rollback

↓

Safe Recovery

Warnings

↓

Logged

↓

Import Continues

---

# Development Rules

The Import Engine shall

Never modify original TXT files.

Never overwrite imported raw data.

Never perform engineering corrections before validation.

Never bypass SQLite transactions.

---

# Future Expansion

Supported

Single TXT Import

Reserved

Batch Import

Cloud Import

PLC Live Import

Remote Import

---

# Status

04_DataImport

Development Status

✔ Complete

Ready for integration with

05_Engineering

---

End of Document
