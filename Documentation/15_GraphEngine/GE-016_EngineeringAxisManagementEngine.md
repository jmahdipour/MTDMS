# Engineering Axis Management Engine

Document ID : MTDMS-GE-016

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

The Engineering Axis Management Engine is responsible for configuring and maintaining all chart axes used throughout MTDMS.

It guarantees that engineering graphs always display the correct engineering units, scales, limits, labels, and orientation appropriate for the selected test type and standard.

The engine performs **no engineering calculations**.

---

# Objectives

The Axis Management Engine shall

• Configure engineering axes

• Display correct engineering units

• Control scaling

• Synchronize graph appearance

• Support administrator customization

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Axis Configuration

↓

Engineering Graph

Axis configuration affects only visualization.

Engineering values remain unchanged.

---

# Supported Axes

Horizontal Axis (Primary)

Vertical Axis (Primary)

Secondary Horizontal Axis (optional)

Secondary Vertical Axis (optional)

Reference Axis (future)

---

# Supported X-Axis Variables

Time

Engineering Strain

True Strain

Displacement

Extension

Crosshead Position

Pipe Deflection

Administrator configurable.

---

# Supported Y-Axis Variables

Force

Engineering Stress

True Stress

Spring Force

Ring Load

Compression Stress

Flexural Stress

Administrator configurable.

---

# Units

Supported engineering units include

N

kN

kgf

MPa

GPa

mm

µm

%

s

°C (future)

The displayed unit is automatically determined from the calculation profile.

---

# Axis Scaling

Supported modes

Automatic

Manual

Locked

Normalized

Scientific

Logarithmic (future)

Administrator configurable.

---

# Automatic Limits

The engine may automatically determine

Minimum

Maximum

Tick Interval

Minor Interval

based on the engineering dataset.

---

# Locked Limits

Administrators may define fixed limits

Example

Stress

0–1000 MPa

Strain

0–50 %

These limits are applied regardless of the current dataset.

---

# Tick Marks

Supported

Major

Minor

Inside

Outside

Cross

Administrator configurable.

---

# Grid Association

Major gridlines

Minor gridlines

are synchronized with the selected tick intervals.

---

# Axis Labels

Automatically generated

Example

Engineering Stress (MPa)

Engineering Strain (%)

Force (N)

Displacement (mm)

The labels are localized according to the application language.

---

# Axis Direction

Supported

Normal

Reversed

Administrator configurable.

Typical engineering graphs use the normal direction.

---

# Zero Crossing

The engine shall support

Automatic

Zero

Minimum

Maximum

Administrator configurable.

---

# Multi-Axis Charts

Supported

Primary + Secondary Y

Primary + Secondary X

The secondary axes are used only when required by the graph template.

---

# Engineering Independence

The Axis Management Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Only axis presentation is affected.

---

# SQLite Interaction

SQLite stores

Axis Profiles

Default Units

Scaling Preferences

Administrator Settings

No engineering values are modified.

---

# Error Handling

Missing Axis Profile

↓

Use Default

Invalid Unit

↓

Use SI Unit

Axis Overflow

↓

Auto Scale

Invalid Tick Interval

↓

Calculate Automatically

---

# Performance Targets

Axis Configuration

< 20 ms

Axis Refresh

< 50 ms

Complete Axis Update

< 100 ms

---

# Acceptance Criteria

✔ Automatic unit selection

✔ Automatic scaling

✔ Manual scaling

✔ Multi-axis support

✔ Localized labels

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
