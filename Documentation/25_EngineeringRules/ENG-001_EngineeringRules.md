# Engineering Rules

Document ID

MTDMS-ENG-001

Version

1.0

Status

Frozen

Application

MTDMS

---

# Purpose

This document defines the engineering rules that every module inside MTDMS must follow.

These rules cannot be overridden by programming decisions.

---

# Rule 1

Original Data Never Changes

TXT

↓

Read Only

Raw Arrays

↓

Read Only

No engine may modify raw arrays.

---

# Rule 2

Every Engineering Result Must Be Reproducible

Given

Same TXT

Same Settings

Same Version

↓

Exactly Same Result

100%

Repeatability

---

# Rule 3

Every Result Must Be Traceable

Every calculated value shall have

Source

Method

Engine

Version

Timestamp

SessionID

---

# Rule 4

No Hidden Engineering Decisions

Software never guesses.

Software never changes method automatically.

Operator decides.

Software records.

---

# Rule 5

Every Engineering Calculation Must Be Independent

Stress Engine

does not know

Young Engine

Young Engine

does not know

Yield Engine

Every engine performs exactly one task.

---

# Rule 6

Every Dataset Has Only One Truth

EngineeringDataset

is

the only engineering source.

TXT

Worksheet

SQLite

never become engineering references.

---

# Rule 7

Raw Data Are Sacred

Force

Time

Crosshead

Extensometer

never modified

never filtered

never smoothed

never corrected

Only copied.

---

# Rule 8

Derived Data Are Independent

Stress

Strain

CorrectedStrain

TrueStress

TrueStrain

may be regenerated

at any time.

---

# Rule 9

Graph Is Visualization

Graph

never changes data.

Graph

reads data.

Only.

---

# Rule 10

Report Is Read Only

Report

never calculates.

Report

never corrects.

Report

only displays.

---

# Rule 11

Database Is Archive

SQLite

stores

results

metadata

audit

never calculations.

---

# Rule 12

Settings Are Frozen During Session

Session starts

↓

Settings copied

↓

Calculation

↓

Settings unchanged

---

# Rule 13

Units Never Change Internally

Internal Force

kgf

Internal Length

mm

Internal Stress

kgf/mm²

Conversions

performed only

inside Report Engine.

---

# Rule 14

One Point

One Meaning

Index i

always represents

exactly one physical measurement.

Every array shares the same index.

---

# Rule 15

No Silent Failure

Every failure

must produce

Error

Warning

Audit

Log

Nothing fails silently.

---

# Rule 16

Engineering Before Programming

Whenever engineering and implementation conflict,

engineering wins.

---

# Rule 17

ISO 17025 Priority

If an implementation shortcut conflicts with

ISO 17025,

the shortcut is rejected.

---

# Rule 18

Backward Compatibility

A newer version of MTDMS shall always be capable of reading results produced by previous versions.

---

# Rule 19

Deterministic Execution

The calculation order is fixed.

No engine changes execution sequence.

---

# Rule 20

Version Controlled Results

Every report stores

Software Version

Calculation Version

Rule Version

Material Library Version

Settings Version

---

# Acceptance

✔ Engineering First

✔ Deterministic

✔ Reproducible

✔ Traceable

✔ ISO 17025 Ready

✔ Future Proof

---

End Of Document
