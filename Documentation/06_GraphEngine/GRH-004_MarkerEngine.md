# Marker Engine

Document ID : MTDMS-GRH-004

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Graph Engine

Status

Production

---

# Purpose

This document defines the Marker Engine responsible for creating, displaying, editing and managing graphical markers on engineering curves.

Markers identify important engineering events without modifying the original data.

Typical markers include

• Yield Point

• Ultimate Tensile Strength

• Necking

• Fracture

• Elastic Region

• User-defined Points

• Maximum

• Minimum

• Intersection Points

---

# Design Philosophy

Markers are

Visualization Objects

Only.

Markers shall

never

modify

Engineering Data

Raw Data

Calculated Results

---

# Marker Architecture

```
Graph

↓

Curve

↓

Marker Layer

↓

Marker Object

↓

Display
```

---

# Marker Object

Each marker contains

ID

Type

Curve ID

Sample Index

X Coordinate

Y Coordinate

Label

Visibility

Color

Size

Locked Status

Created By

Timestamp

---

# Supported Marker Types

Automatic

Yield

Upper Yield

Lower Yield

Rp

Rt

Ultimate Tensile Strength

Necking

Fracture

Elastic Region Start

Elastic Region End

Maximum

Minimum

---

Manual

Operator Marker

Reference Marker

Measurement Marker

Inspection Marker

Reserved Marker

---

# Marker Identification

Every marker has a unique identifier

Example

```
MKR-000001
```

IDs remain unchanged during editing.

---

# Marker Rendering

Marker

↓

Symbol

↓

Label

↓

Leader Line

↓

Tooltip

---

# Marker Symbols

Circle

Square

Triangle

Diamond

Cross

Star

Arrow

Administrator configurable.

---

# Marker Colors

Default

Yield

Green

UTS

Red

Fracture

Black

Necking

Orange

Manual

Blue

Reference

Gray

User configurable.

---

# Marker Labels

Displayed

Name

Stress

Strain

Force

Extension

Time

Units

Optional

---

# Marker Behaviour

Marker

moves automatically

if graph scaling changes.

Marker

shall remain attached

to

Engineering Sample

not

Screen Position.

---

# Marker Editing

Operator may

Move Marker

Delete Marker

Rename Marker

Change Color

Lock Marker

Hide Marker

Duplicate Marker

---

# Locked Marker

Engineering markers

may be locked.

Locked markers

cannot be moved accidentally.

---

# Marker Selection

Single Click

Select

Double Click

Edit

Right Click

Context Menu

---

# Context Menu

Edit

Delete

Hide

Copy Coordinates

Export

Lock

Unlock

Properties

---

# Tooltip

Mouse Hover

Displays

Marker Name

Engineering Values

Sample Number

Time

Notes

---

# Undo / Redo

All marker operations

shall support

Undo

Redo

without affecting engineering calculations.

---

# Database Storage

SQLite

Table

```
tblGraphMarkers
```

Fields

MarkerID

CurveID

MarkerType

SampleIndex

XValue

YValue

Label

Visible

Locked

Color

Operator

Timestamp

---

# Report Behaviour

Engineering Report

Shows

Yield

UTS

Fracture

Necking

Only.

Temporary construction markers

shall be hidden automatically.

---

# Performance

Supports

1000+ markers

without visible slowdown.

Marker movement

shall update

in real time.

---

# Error Handling

Invalid Sample Index

↓

Reject Marker

Curve Missing

↓

Hide Marker

Duplicate ID

↓

Generate New ID

Overflow

↓

Abort

Rollback

---

# Future Enhancements

Smart Marker Detection

AI Marker Suggestion

Grouped Markers

Marker Templates

3D Marker Support

Reserved

---

# Acceptance Criteria

✔ Engineering markers supported

✔ Manual markers supported

✔ Undo / Redo

✔ Locked markers

✔ Real-time movement

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering data never modified

---

End of Document
