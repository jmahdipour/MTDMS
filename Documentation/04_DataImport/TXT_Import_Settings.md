# TXT Import Settings

Document ID : MTDMS-IMP-014

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

---

# Purpose

This document defines every configurable option available for the TXT Import System.

All settings are stored inside the workbook and may optionally be synchronized with SQLite.

The operator shall configure these settings through the Ribbon only.

No worksheet editing is permitted.

---

# Settings Architecture

Ribbon

↓

Settings Controller

↓

Import Settings

↓

Workbook Settings

↓

SQLite (Optional)

---

# Import Settings Categories

General

File

Header

Units

Validation

Performance

Engineering

Database

Logging

Advanced

---

# General Settings

## Default TXT Folder

Description

Default folder opened by Browse TXT.

Default

Last Used Folder

Supported

Absolute Path

Relative Path

Network Path

---

## Remember Last Folder

Type

Boolean

Default

True

---

## Automatically Preview TXT

Type

Boolean

Default

True

---

## Automatically Validate After Import

Type

Boolean

Default

True

---

## Automatically Calculate

Type

Boolean

Default

False

---

# File Settings

## Maximum File Size

Default

100 MB

Recommended

20 MB

---

## Maximum Row Count

Default

500000

---

## Supported Encoding

Auto

UTF-8

ANSI

UTF-16

Default

Auto

---

## Delimiter Detection

Auto

Tab

Comma

Semicolon

Space

Default

Auto

---

# Header Settings

Require Machine Name

Default

True

---

Require Material

Default

True

---

Require Standard

Default

True

---

Require Gauge Length

Default

True

---

Require Area

Default

True

---

Allow Unknown Header Fields

Default

True

---

# Unit Settings

Automatic Unit Detection

Default

True

---

Automatic Unit Conversion

Default

True

---

Internal Force Unit

Newton

---

Internal Length Unit

Millimeter

---

Internal Stress Unit

MPa

---

Internal Time Unit

Second

---

# Validation Settings

Ignore Blank Lines

Default

True

---

Ignore Duplicate Rows

Default

True

---

Stop On Header Error

Default

True

---

Stop On Unit Error

Default

True

---

Stop On Data Error

Default

False

---

Engineering Plausibility Check

Default

True

---

# Performance Settings

Disable Screen Updating

Default

True

---

Disable Events

Default

True

---

Manual Calculation Mode

Default

True

---

Buffered Import

Default

True

---

Progress Indicator

Default

Status Bar

---

# Engineering Settings

Use Material Library

Default

True

---

Use Standard Library

Default

True

---

Automatic Area Calculation

Default

True

---

Automatic Stress Calculation

Default

True

---

Automatic Strain Calculation

Default

True

---

Automatic True Stress Calculation

Default

True

---

Automatic True Strain Calculation

Default

True

---

# Database Settings

Store Raw TXT

Default

True

---

Store Import History

Default

True

---

Store Import Performance

Default

True

---

Automatic SQLite Backup

Default

False

---

# Logging Settings

Import Log

Enabled

---

Validation Log

Enabled

---

Performance Log

Enabled

---

Error Log

Enabled

---

Debug Log

Disabled

---

# Advanced Settings

Machine Profile

Automatic

---

Parser Mode

Standard

Future

Fast Parser

Streaming Parser

---

Developer Mode

Default

False

---

Show Internal Import Statistics

Default

False

---

# Settings Storage

Workbook

↓

Hidden Configuration Sheet

↓

SQLite (Optional)

---

# Reset Settings

Button

Restore Defaults

Restores

Factory Configuration

Does not affect

Projects

Database

Reports

Material Library

---

# Future Settings

Cloud Import

Batch Import

Automatic Machine Recognition

AI Import Assistant

Reserved

---

# Acceptance Criteria

✔ Settings editable from Ribbon only

✔ Persist between sessions

✔ Compatible with Excel 2019

✔ Compatible with SQLite

✔ No worksheet interaction required

✔ No UserForm required

---

End of Document
