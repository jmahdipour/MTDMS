# Graph Configuration Database

Document ID : MTDMS-DB-014

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

The Graph Configuration Database stores all configuration parameters related to graph generation inside MTDMS.

It defines how engineering graphs are displayed.

It never changes engineering calculations.

It never modifies imported TXT data.

---

# Objectives

The Graph Configuration Database shall

• Store graph appearance

• Store graph defaults

• Store graph correction options

• Store graph export options

• Preserve graph consistency

---

# Design Philosophy

TXT

↓

Engineering Calculation

↓

Engineering Data

↓

Graph Configuration

↓

Excel Chart

Configuration changes

display only.

Engineering values remain unchanged.

---

# Table Name

tblGraphConfiguration

---

# Primary Key

GraphConfigID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

GraphConfigID

INTEGER

----------------------------

GraphType

TEXT

Examples

Stress-Strain

Force-Displacement

Force-Time

Extension-Time

Spring

Ring Stiffness

Custom

----------------------------

ChartType

TEXT

Examples

XY Scatter

Line

Smooth Line

----------------------------

XAxisTitle

TEXT

----------------------------

YAxisTitle

TEXT

----------------------------

XAxisUnit

TEXT

----------------------------

YAxisUnit

TEXT

----------------------------

ShowGrid

BOOLEAN

----------------------------

ShowLegend

BOOLEAN

----------------------------

ShowMarkers

BOOLEAN

----------------------------

MarkerSize

INTEGER

----------------------------

LineWidth

REAL

----------------------------

LineColor

TEXT

RGB or HEX

----------------------------

BackgroundColor

TEXT

----------------------------

BorderColor

TEXT

----------------------------

ChartFont

TEXT

----------------------------

ChartFontSize

INTEGER

----------------------------

AutoScale

BOOLEAN

----------------------------

MaintainAspectRatio

BOOLEAN

----------------------------

EnableMouseCoordinates

BOOLEAN

----------------------------

EnableYieldMarker

BOOLEAN

----------------------------

EnableFractureMarker

BOOLEAN

----------------------------

EnableMaximumMarker

BOOLEAN

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

# Supported Graph Types

Stress-Strain

Force-Displacement

Force-Time

Displacement-Time

Extension-Time

Spring Force-Extension

Ring Stiffness

Custom

Administrator configurable.

---

# Graph Display Rules

Engineering graph

shall always display

validated data only.

Construction lines

shall never appear

in the final report.

---

# Automatic Scaling

Supported

Automatic

Manual

User Defined

Administrator configurable.

---

# Mouse Interaction

Supported

Coordinate Display

Point Selection

Yield Selection

Fracture Selection

Zoom

Pan

---

# Engineering Independence

Graph configuration

shall never

change

Engineering Results

Engineering Tables

Material Properties

Validation Results

---

# Graph Export

Configuration supports

Excel Chart

PDF

Image

Clipboard

---

# SQLite Relationships

tblGraphConfiguration

↓

Referenced by

Graph Engine

Report Engine

Export Engine

---

# Indexes

IX_GraphType

IX_ChartType

---

# Constraints

GraphType

Required

ChartType

Required

---

# Audit Trail

Store

Graph Type

Parameter

Old Value

New Value

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

Missing Configuration

↓

Load Defaults

Invalid Color

↓

Use Default Color

Invalid Font

↓

Use Default Font

Unknown Graph Type

↓

Abort

---

# Performance

Graph configuration loading

Target

< 50 ms

---

# Acceptance Criteria

✔ Graph defaults stored

✔ User customization supported

✔ Engineering calculations unaffected

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
