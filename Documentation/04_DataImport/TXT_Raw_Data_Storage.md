# TXT Raw Data Storage Specification

Document ID : MTDMS-IMP-027

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Database

SQLite

---

# Purpose

This document defines how imported TXT data shall be stored before any engineering calculations.

Raw data is the only authoritative source of imported measurements.

Engineering calculations shall never overwrite raw data.

---

# Philosophy

```
TXT

↓

Parser

↓

Raw Data

↓

Engineering Data
