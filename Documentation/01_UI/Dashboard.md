# Dashboard Specification

Document ID : MTDMS-UI-008

Version : 0.1.0

Platform

Microsoft Excel 2019

Ribbon XML

Workbook

WorkbookTemplate.xlsm

---

# Purpose

The Dashboard is the HOME worksheet.

It is the application's control center.

No engineering calculations are performed here.

Its purpose is

• Navigation

• Project Management

• Quick Status

• Recent Projects

• Laboratory Information

---

# Worksheet

HOME

---

# Design Principle

The Dashboard must resemble professional industrial software.

It must NOT resemble an Excel worksheet.

---

# Layout

```
┌────────────────────────────────────────────────────────────┐
│                    HEADER                                  │
├────────────────────────────────────────────────────────────┤
│                                                            │
│  Project Panel       Quick Actions      System Status       │
│                                                            │
├────────────────────────────────────────────────────────────┤
│                                                            │
│               Recent Projects                              │
│                                                            │
├────────────────────────────────────────────────────────────┤
│                                                            │
│ Material Library     Standard Library     Machine Status    │
│                                                            │
├────────────────────────────────────────────────────────────┤
│                                                            │
│                    FOOTER                                  │
└────────────────────────────────────────────────────────────┘
```

---

# Header

Contains

Application Name

Current Project

Current Material

Current Standard

Current Operator

Date

Time

Workbook Version

---

# Project Panel

Displays

Project Name

Customer

Operator

Machine

Specimen

Material

Standard

Project Status

---

# Quick Actions

Buttons

Import TXT

Open Project

Save Project

Generate Report

Graph

Settings

---

# Recent Projects

Displays

Last 10 Projects

Information

Project Name

Material

Date

Status

Double Click

Open Project

---

# Material Library Summary

Displays

Current Material

Young's Modulus

Yield Strength

Ultimate Strength

Density

---

# Standard Library Summary

Displays

Current Standard

Offset Method

Calculation Method

Reference

---

# Machine Status

Displays

TXT Loaded

Database Connected

Workbook Status

Calculation Status

Report Status

---

# Status Indicators

Green

Ready

Blue

Busy

Yellow

Warning

Red

Error

Gray

Offline

---

# Footer

Displays

Workbook Version

Database Version

Git Revision

SQLite Status

Excel Version

Operating System

---

# Button Style

Rounded Rectangle

Width

140 px

Height

36 px

Icon

32 px

Caption

Below Icon

---

# Dashboard Refresh

Automatically updates

Project Information

Material

Status

Time

Recent Projects

No user action required.

---

# Double Click Actions

Recent Project

↓

Open Project

Material

↓

Open Material Library

Standard

↓

Open Standard Library

---

# Security

Dashboard is protected.

Only input controls remain unlocked.

---

# Performance

Dashboard refresh

< 300 ms

No calculations shall execute during dashboard refresh.

---

# Future

Laboratory Logo

Company Logo

Dark Theme

Favorite Projects

Pinned Projects

Notification Center

License Information

Cloud Status

---

End of Document
