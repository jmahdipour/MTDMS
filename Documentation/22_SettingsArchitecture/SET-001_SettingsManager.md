# Settings Manager Architecture

Document ID

MTDMS-SET-001

Version

1.0

Status

Core Architecture

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

---

# Purpose

Settings Manager stores every configurable option used inside MTDMS.

Every engine reads its configuration only from this object.

No engine stores local settings.

---

# Architecture

Application

↓

Settings Manager

↓

Calculation Engine

↓

Graph Engine

↓

Report Engine

↓

Archive Engine

---

# Design Principle

Single Source Of Configuration

Only one object stores settings.

---

# Main Class

clsSettingsManager

Contains

Application

Calculation

Graph

Import

Material

Report

Archive

User

---

# Object Structure

SettingsManager

│

├── ApplicationSettings

├── ImportSettings

├── CalculationSettings

├── MaterialSettings

├── GraphSettings

├── ReportSettings

├── ArchiveSettings

├── UserSettings

└── DebugSettings

---

# Application Settings

Contains

Language

Theme

Autosave

Temporary Folder

Backup Folder

Logging

---

# Import Settings

Contains

TXT Encoding

Decimal Separator

Field Separator

Maximum Point Count

Import Validation

---

# Calculation Settings

Contains

Strain Source

Crosshead

Extensometer

--------------------------------

Yield Method

Rp0.2

Rp0.1

Rt

Upper Yield

Lower Yield

Manual

--------------------------------

Young Modulus Method

Automatic Regression

Manual

Standard

--------------------------------

True Stress Enabled

--------------------------------

True Strain Enabled

--------------------------------

Fracture Detection Method

Automatic

Manual

--------------------------------

Curve Correction Enabled

---

# Material Settings

Contains

Material Library

Material Category

Default Young

Default Yield

Area Calculation

Administrator configurable

---

# Graph Settings

Contains

Graph Theme

Marker Size

Line Width

Colors

Grid

Zoom

Cursor

Yield Marker

Fracture Marker

---

# Report Settings

Contains

Logo

Company

Language

Unit System

Header

Footer

Page Size

A4

Landscape

Portrait

Summary Tables

INSO 3132

Mabhas 9

Administrator configurable

---

# Archive Settings

Contains

SQLite Path

Backup Interval

CSV Export

PDF Export

Automatic Archive

---

# User Settings

Contains

Operator Name

Operator ID

Laboratory

Permissions

---

# Debug Settings

Contains

Enable Debug

Execution Log

Performance Timer

Memory Usage

Verbose Logging

---

# Rule

Every Engine

↓

reads

↓

SettingsManager

No Engine modifies settings.

Only UI modifies settings.

---

# Session

Settings are copied

into Session

at Session Start.

Changes after Session Start

do not affect

current calculation.

---

# Persistence

Settings

↓

SQLite

↓

Application Start

↓

Load

↓

Memory

---

# Validation

Settings checked

before Session Start.

---

# Acceptance

✔ Centralized

✔ Modular

✔ Thread Safe Ready

✔ Excel Independent

✔ SQLite Compatible

✔ Future VB.NET Compatible

---

End Of Document
