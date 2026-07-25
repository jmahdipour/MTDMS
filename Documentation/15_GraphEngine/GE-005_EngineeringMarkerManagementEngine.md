# Engineering Marker Management Engine

Document ID : MTDMS-GE-005

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Chart Technology

Microsoft Excel Chart Objects

Database

SQLite

Primary Data Source

TXT File

Application

MTDMS

Status

Production

---

# Purpose

The Engineering Marker Management Engine is responsible for creating, displaying, validating, storing, and managing all engineering markers shown on graphs.

Markers are engineering annotations only.

They do not modify the engineering calculations.

---

# Objectives

The Marker Engine shall

• Create engineering markers

• Manage marker visibility

• Validate marker positions

• Support automatic and manual markers

• Maintain complete traceability

---

# Engineering Philosophy

Engineering Dataset

↓

Engineering Marker

↓

Operator Review

↓

Engineering Report

Markers describe engineering results.

They never replace engineering calculations.

---

# Marker Categories

Automatic Markers

Manual Markers

Reference Markers

Temporary Markers

Validation Markers

Inspection Markers

Administrator configurable.

---

# Automatic Markers

Automatically generated markers include

Yield Point

Maximum Force

Ultimate Tensile Strength

Fracture Point

Elastic Region

Reference Deformation

Maximum Compression

Spring Constant Region

Ring Stiffness Reference

---

# Manual Markers

The operator may manually create

Yield Point

Fracture Point

Inspection Point

Reference Point

Comment Point

Every manual marker is logged.

---

# Marker Information

Each marker stores

Unique Marker ID

Marker Type

X Coordinate

Y Coordinate

Engineering Value

Creation Time

Operator

Visibility Status

Validation Status

---

# Marker Validation

The engine shall verify

Marker on Dataset

Marker inside Graph Limits

Engineering Meaning

Selected Graph Type

Duplicate Marker

---

# Marker Visibility

Supported modes

Visible

Hidden

Report Only

Screen Only

Administrator configurable.

---

# Report Behaviour

The following markers may appear in reports

Yield

Ultimate Strength

Fracture

Reference Deformation

Construction markers

shall remain hidden unless explicitly enabled.

---

# Temporary Markers

Temporary markers

may be used during

Inspection

Graph Analysis

Zoom

Measurement

These markers are automatically removed after the session ends.

---

# Marker Editing

The operator may

Move Marker

Rename Marker

Delete Marker

Hide Marker

Show Marker

Every action is recorded.

---

# Marker Locking

Certain markers

generated automatically

may be protected from editing

depending on

Administrator Settings.

---

# Marker Styles

Marker Shape

Marker Size

Marker Color

Label Position

Leader Line

obtained from

Graph Style Library.

---

# Engineering Independence

The Marker Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Only graphical annotations are managed.

---

# SQLite Interaction

SQLite stores

Marker Metadata

Operator Actions

Visibility

Audit Information

Marker Styles

Engineering values remain unchanged.

---

# Error Handling

Marker Outside Dataset

↓

Reject

Duplicate Marker

↓

Warning

Invalid Marker Type

↓

Reject

Locked Marker

↓

Editing Denied

---

# Performance Targets

Marker Creation

< 20 ms

Marker Update

Immediate

Marker Validation

< 20 ms

---

# Acceptance Criteria

✔ Automatic markers supported

✔ Manual markers supported

✔ Marker validation supported

✔ Marker locking supported

✔ Report visibility control

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete audit trace

---

End of Document
