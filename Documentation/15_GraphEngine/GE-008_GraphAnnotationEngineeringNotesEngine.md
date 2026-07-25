# Graph Annotation & Engineering Notes Engine

Document ID : MTDMS-GE-008

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

The Graph Annotation & Engineering Notes Engine allows engineers to attach technical notes, labels, callouts, and annotations to engineering graphs generated from validated datasets.

Annotations are informational only.

They never influence engineering calculations.

---

# Objectives

The Annotation Engine shall

• Add engineering notes

• Add technical labels

• Add inspection comments

• Preserve annotation history

• Support report annotations

---

# Engineering Philosophy

Engineering Dataset

↓

Graph

↓

Engineering Annotation

↓

Engineering Review

↓

Report

Annotations document engineering observations.

They never alter engineering results.

---

# Annotation Types

Engineering Note

Inspection Note

Operator Comment

Warning

Observation

Reference Label

Marker Description

Customer Comment

Administrator configurable.

---

# Annotation Sources

Manual

Automatic

Imported Metadata

Validation Messages

Material Library

Administrator configurable.

---

# Supported Locations

Free Position

Attached to Marker

Attached to Data Point

Attached to Axis

Attached to Graph Title

Attached to Legend

---

# Annotation Content

Each annotation may contain

Title

Description

Engineering Comment

Operator

Timestamp

Priority

Reference

Attachment ID (future)

---

# Automatic Annotations

The engine may automatically create annotations for

Yield Point

Ultimate Strength

Fracture Point

Reference Deformation

Validation Warning

Material Comparison

Administrator configurable.

---

# Manual Notes

The operator may insert

Engineering Explanation

Customer Remark

Inspection Result

Failure Description

Laboratory Observation

Each note is recorded in the audit trail.

---

# Visibility Modes

Visible

Hidden

Report Only

Screen Only

Administrator configurable.

---

# Report Behaviour

Report templates may include

Engineering Notes

Inspection Comments

Validation Remarks

Customer Remarks

Construction annotations shall remain hidden unless explicitly enabled.

---

# Editing

The operator may

Move

Edit

Hide

Delete

Duplicate

Engineering Notes

Every modification is recorded.

---

# Annotation Styles

Text Font

Text Size

Text Color

Border

Leader Line

Background

obtained from

Graph Style Library.

---

# Engineering Independence

The Annotation Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Only graphical information is managed.

---

# SQLite Interaction

SQLite stores

Annotation Text

Operator

Timestamp

Visibility

Style

Audit Information

Engineering values remain unchanged.

---

# Error Handling

Invalid Annotation Position

↓

Reject

Missing Graph

↓

Abort

Locked Annotation

↓

Editing Denied

Missing Style

↓

Use Default

---

# Performance Targets

Annotation Creation

< 20 ms

Annotation Update

Immediate

Annotation Refresh

< 20 ms

---

# Acceptance Criteria

✔ Engineering notes supported

✔ Automatic annotations supported

✔ Manual annotations supported

✔ Report visibility control

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
