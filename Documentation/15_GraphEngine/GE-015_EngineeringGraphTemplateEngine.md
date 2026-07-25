# Engineering Graph Template Engine

Document ID : MTDMS-GE-015

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

TXT File (Testing Machine Export)

Application

MTDMS

Status

Production

---

# Purpose

The Engineering Graph Template Engine provides standardized graph templates for every supported mechanical test.

Instead of configuring each chart manually, the system automatically applies the appropriate template based on the selected test type and engineering standard.

This ensures that all graphs have a consistent appearance, axis definitions, units, colors, annotations, and layout across the entire application.

The engine performs **no engineering calculations**.

---

# Objectives

The Graph Template Engine shall

• Automatically select graph templates

• Standardize engineering presentation

• Reduce operator configuration

• Ensure report consistency

• Support administrator customization

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Graph Template

↓

Excel Chart

↓

Engineering Review

Graph appearance is determined entirely by the template.

Engineering values remain unchanged.

---

# Template Selection

Templates are selected automatically using

Test Type

Selected Standard

Material Category

Graph Type

Administrator Rules

---

# Supported Templates

Tensile Test

Compression Test

Three-Point Bending

Four-Point Bending

Spring Constant

Ring Stiffness

Raw Machine Data

Comparison Graph

Overlay Graph

Statistical Trend

Administrator configurable.

---

# Template Components

Each template defines

Graph Title

X Axis

Y Axis

Units

Axis Scale

Grid

Legend

Fonts

Colors

Markers

Annotations

Margins

Print Layout

---

# Axis Definitions

Example

### Tensile

X

Engineering Strain (%)

Y

Engineering Stress (MPa)

----------------------------

### Spring

X

Displacement (mm)

Y

Force (N)

----------------------------

### Ring Stiffness

X

Deflection (mm)

Y

Force (N)

---

# Automatic Units

Units are selected automatically from the engineering calculation profile.

Examples

N

kN

MPa

GPa

mm

%

s

Administrator configurable.

---

# Automatic Scaling

Each template defines

Minimum Axis

Maximum Axis

Auto Scale

Locked Scale

Scientific Format

Logarithmic (future)

---

# Marker Rules

Templates define which engineering markers are displayed.

Example

### Tensile

Yield

Ultimate

Fracture

Elastic Region

----------------------------

### Spring

Linear Region

Regression

Maximum Force

---

# Print Templates

Separate print templates may exist for

Laboratory Report

Certificate

Customer Report

Presentation

PDF

---

# Administrator Customization

Administrators may create

New Templates

Duplicate Templates

Modify Existing Templates

Assign Templates

Export Templates

Import Templates

---

# Template Versioning

Every template stores

Template ID

Version

Creation Date

Author

Revision

Approval

---

# Engineering Independence

The Graph Template Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Only presentation rules are applied.

---

# SQLite Interaction

SQLite stores

Template Definitions

Template Versions

Assignments

Administrator Changes

Audit History

Templates are loaded dynamically during graph generation.

---

# Error Handling

Missing Template

↓

Use Default Template

Invalid Template

↓

Reject

Missing Units

↓

Use Calculation Profile

Template Version Conflict

↓

Use Latest Approved Version

---

# Performance Targets

Template Selection

< 20 ms

Template Application

< 100 ms

Complete Graph Generation

< 500 ms

---

# Acceptance Criteria

✔ Automatic template selection

✔ Standardized engineering presentation

✔ Administrator customization

✔ Template version control

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
