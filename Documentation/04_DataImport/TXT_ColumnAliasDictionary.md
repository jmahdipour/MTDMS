# TXT Column Alias Dictionary

Document ID : MTDMS-IMP-039

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Application

MTDMS

---

# Purpose

This document defines every supported data-column alias that may appear inside TXT files.

Unlike Header Alias Dictionary, this document is only responsible for the columns containing measured test data.

Different testing machines use different names for identical signals.

The parser converts every recognized alias into one internal engineering variable.

---

# Architecture

TXT Column

↓

Alias Dictionary

↓

Internal Variable

↓

Engineering Engine

↓

Graph Engine

↓

Report Engine

---

# Storage

SQLite

Table

```
tblColumnAlias
```

---

# Table Structure

| Alias | Internal Variable | Unit Type | Required |
|--------|-------------------|-----------|----------|
| Force | Force | Force | Yes |
| Load | Force | Force | Yes |

---

# Rules

Matching

Case Insensitive

Unicode Supported

Multiple Aliases Allowed

Internal Variable

Unique

---

# Primary Engineering Columns

Time

Force

Stroke

Extension

Stress

Strain

Temperature

Speed

Reserved Channels

---

# Time

Accepted Aliases

Time

TIME

Elapsed Time

Test Time

Seconds

Second

sec

t

Time(s)

Internal Variable

```
Time
```

Unit

Second

---

# Force

Accepted Aliases

Force

FORCE

Load

LOAD

Applied Force

Testing Force

Test Load

Load Cell

Channel Force

F

Internal Variable

```
Force
```

Preferred Unit

Newton

---

# Stroke

Accepted Aliases

Stroke

Crosshead

Crosshead Position

Displacement

Travel

Ram Position

Head Position

CH Position

Machine Stroke

Internal Variable

```
Stroke
```

Preferred Unit

Millimeter

---

# Extension

Accepted Aliases

Extension

Elongation

Extensometer

Gauge Extension

Gauge Elongation

Extension(mm)

Strain Length

Internal Variable

```
Extension
```

Preferred Unit

Millimeter

---

# Engineering Stress

Accepted Aliases

Stress

Engineering Stress

Sigma

σ

Internal Variable

```
Stress
```

Preferred Unit

MPa

---

# Engineering Strain

Accepted Aliases

Strain

Engineering Strain

Epsilon

ε

Internal Variable

```
Strain
```

Preferred Unit

mm/mm

---

# True Stress

Accepted Aliases

True Stress

Real Stress

Internal Variable

```
TrueStress
```

---

# True Strain

Accepted Aliases

True Strain

Real Strain

Internal Variable

```
TrueStrain
```

---

# Temperature

Accepted Aliases

Temperature

Temp

°C

Temp(C)

Internal Variable

```
Temperature
```

Preferred Unit

Degree Celsius

---

# Speed

Accepted Aliases

Speed

Crosshead Speed

Test Speed

Velocity

Rate

Internal Variable

```
Speed
```

Preferred Unit

mm/min

---

# Cycle

Future

Accepted Aliases

Cycle

Cycles

Count

Internal Variable

```
Cycle
```

Reserved

---

# Pressure

Future

Accepted Aliases

Pressure

Hydraulic Pressure

Oil Pressure

Internal Variable

```
Pressure
```

Reserved

---

# Torque

Future

Accepted Aliases

Torque

Moment

Nm

Internal Variable

```
Torque
```

Reserved

---

# Reserved Channels

Machines may export

Channel1

Channel2

Channel3

AI1

AI2

Encoder

PLC Register

These channels

are imported

but ignored

unless mapped manually.

---

# Unknown Columns

Unknown column

↓

Ignored

↓

Logged

↓

Stored in Audit Trail

Import continues.

---

# Duplicate Columns

Example

```
Force

Load
```

Parser selects

Higher Priority Alias

Second column

Logged

Ignored

---

# Administrator Functions

Administrator may

Add Alias

Disable Alias

Export Dictionary

Import Dictionary

Modify Priority

Without changing VBA code.

---

# Acceptance Criteria

✔ Unlimited aliases

✔ SQLite configurable

✔ Case insensitive

✔ Unicode supported

✔ Supports all machine manufacturers

✔ Excel 2019 compatible

---

End of Document
