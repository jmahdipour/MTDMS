# MTDMS Development Roadmap

Document ID : MTDMS-RDM-001

Platform

Microsoft Excel 2019

Language

VBA

Ribbon XML

Database

SQLite

Input

TXT Only

---

# Phase 01

Repository

Status

✔ Completed

Deliverables

Repository Structure

Git Flow

Documentation Skeleton

---

# Phase 02

Workbook Design

Status

In Progress

Deliverables

WorkbookTemplate.xlsm

Worksheets

Named Ranges

Tables

Navigation

Protection

Theme

---

Workbook Structure

HOME

IMPORT

ANALYSIS

GRAPH

REPORT

RAW_DATA

ENGINEERING

RESULT

MATERIAL_DB

STANDARD_DB

SETTINGS

SYSTEM

ERROR_LOG

HISTORY

---

# Phase 03

Ribbon Development

Deliverables

Ribbon XML

Callbacks

Ribbon Controller

Icons

Groups

Tabs

---

Ribbon Tabs

Home

Import

Calculation

Graph

Report

Database

Settings

Help

---

# Phase 04

TXT Engine

Deliverables

TXT Parser

TXT Validation

TXT Preview

TXT Mapping

TXT Import

TXT Error Handler

---

# Phase 05

Material Library

Deliverables

Material Database

Material Editor

Material Search

Material Import

Material Export

---

# Phase 06

Calculation Engine

Deliverables

Stress

Strain

Young

Yield

UTS

Fracture

Correction

Regression

Validation

---

# Phase 07

Graph Engine

Deliverables

Stress-Strain Graph

Force-Stroke Graph

Zoom

Pan

Crosshair

Yield Marker

Fracture Marker

Correction

Export

---

# Phase 08

Report Engine

Deliverables

Report Builder

PDF Export

Print

Excel Export

Summary Report

---

# Phase 09

SQLite

Deliverables

Project Database

Material Database

History

Settings

Results

Backup

---

# Phase 10

Testing

Deliverables

TXT Test

Workbook Test

Ribbon Test

Calculation Test

Graph Test

Database Test

Performance Test

---

# Phase 11

Release Candidate

Deliverables

Optimization

Bug Fixes

Documentation

User Manual

Developer Manual

---

# Phase 12

Release

Version

1.0

Deliverables

WorkbookTemplate.xlsm

Ribbon

Database

Documentation

Installation Guide

Release Notes

---

# Long Term

Compression Test

Fatigue Test

Impact Test

Hardness Module

Calibration Module

SPC Module

ISO 17025 Module

Cloud Backup (Optional)

REST API (Optional)

---

# Current Focus

Workbook Design

↓

Ribbon

↓

TXT Parser

↓

Calculation Engine

Everything in the project is driven by the Excel Workbook.

WorkbookTemplate.xlsm is the core of the system.
