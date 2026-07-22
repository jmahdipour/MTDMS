# Graph Style Library

Document ID : MTDMS-DB-030

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Application

MTDMS

Status

Production

---

# Purpose

The Graph Style Library stores all visual styles used for engineering charts generated from imported TXT files.

A Graph Style controls appearance only.

It never changes engineering calculations.

It never changes imported data.

---

# Objectives

The Graph Style Library shall

• Standardize graph appearance

• Support multiple graph themes

• Support customer-specific styles

• Support report styles

• Improve consistency

---

# Design Philosophy

TXT File

↓

Engineering Calculation

↓

Engineering Data

↓

Graph Style

↓

Excel Chart

Only the appearance changes.

Engineering values remain unchanged.

---

# Table Name

tblGraphStyle

---

# Primary Key

GraphStyleID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

GraphStyleID

INTEGER

----------------------------

StyleCode

TEXT

Unique

----------------------------

StyleName

TEXT

----------------------------

ChartType

TEXT

Examples

XY Scatter

Line

Smooth Line

----------------------------

Theme

TEXT

Examples

Laboratory

ISO

Customer

Dark

Light

Custom

----------------------------

BackgroundColor

TEXT

HEX/RGB

----------------------------

PlotAreaColor

TEXT

----------------------------

AxisColor

TEXT

----------------------------

GridColor

TEXT

----------------------------

MainCurveColor

TEXT

----------------------------

SecondaryCurveColor

TEXT

----------------------------

YieldMarkerColor

TEXT

----------------------------

MaximumMarkerColor

TEXT

----------------------------

FractureMarkerColor

TEXT

----------------------------

ConstructionLineColor

TEXT

----------------------------

LineWidth

REAL

----------------------------

MarkerSize

INTEGER

----------------------------

MarkerShape

TEXT

Circle

Square

Diamond

Triangle

----------------------------

FontName

TEXT

----------------------------

FontSize

INTEGER

----------------------------

LegendVisible

BOOLEAN

----------------------------

GridVisible

BOOLEAN

----------------------------

ReportVisible

BOOLEAN

----------------------------

DefaultStyle

BOOLEAN

----------------------------

Active

BOOLEAN

----------------------------

Remarks

TEXT

Nullable

----------------------------

CreatedDate

DATE

----------------------------

ModifiedDate

DATE

----------------------------

ModifiedBy

TEXT

---

# Standard Styles

Laboratory Default

ISO Report

Customer Report

Dark Theme

Light Theme

Presentation Theme

Administrator configurable.

---

# Marker Rules

Construction markers

shall be displayed

during analysis only.

They shall automatically disappear

from

Final Reports

PDF Export

Certificates

---

# Axis Labels

Graph Style

controls only

appearance.

Axis names

and units

are obtained

from

Graph Configuration

and

Unit Database.

---

# Engineering Independence

Graph styles

shall never modify

Engineering Results

Imported TXT

Engineering Tables

Validation Results

---

# SQLite Relationships

tblGraphStyle

↓

Referenced by

Graph Engine

Report Engine

Template Library

---

# Indexes

IX_StyleCode

IX_Theme

IX_DefaultStyle

---

# Constraints

StyleCode

UNIQUE

Theme

Required

ChartType

Required

---

# Audit Trail

Store

Style

Modification

Operator

Timestamp

Computer

Software Version

---

# Permissions

Administrator

Modify

Quality Manager

Modify

Reviewer

Read

Operator

Read Only

---

# Error Handling

Missing Style

↓

Load Default Style

Invalid Color

↓

Load Default Color

Duplicate Style

↓

Reject

Inactive Style

↓

Hidden

---

# Performance

Style loading

Target

< 20 ms

---

# Acceptance Criteria

✔ Multiple graph styles supported

✔ Report styles supported

✔ Construction markers hidden in reports

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Consistent graph appearance

---

End of Document
