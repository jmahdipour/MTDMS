# Report Numbering Engine

Document ID : MTDMS-RE-019

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

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

The Report Numbering Engine generates unique, traceable, and sequential identification numbers for every engineering report, laboratory certificate, and related document produced by MTDMS.

Its purpose is to ensure that every issued document has a permanent identifier that can be traced back to the original engineering dataset and ultimately to the original TXT file.

The engine performs **no engineering calculations**.

---

# Objectives

The Report Numbering Engine shall

• Generate unique report numbers

• Prevent duplicate numbering

• Support configurable numbering formats

• Maintain traceability

• Support ISO/IEC 17025 document control

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Validated Results

↓

Report Number

↓

Engineering Report

Every report shall receive one and only one unique identifier.

---

# Number Generation Workflow

```
Create Report

↓

Determine Document Type

↓

Read Numbering Rule

↓

Generate Next Number

↓

Store in SQLite

↓

Assign to Report
```

---

# Supported Document Types

Engineering Test Report

Laboratory Certificate

Summary Report

Comparison Report

Customer Report

Calibration Report

Administrator configurable.

---

# Default Format

Example

```
TR-2026-000001
```

Where

TR

Report Type

2026

Calendar Year

000001

Sequential Number

---

# Certificate Example

```
TC-2026-000001
```

---

# Number Components

Document Prefix

Year

Month (optional)

Project Code (optional)

Machine Code (optional)

Sequential Counter

Revision (optional)

Administrator configurable.

---

# Revision Number

Revision numbering is managed separately.

Example

```
TR-2026-000125-R00

TR-2026-000125-R01
```

The report number remains constant.

Only the revision changes.

---

# Counter Reset

Supported

Never

Yearly

Monthly

Custom

Administrator configurable.

---

# Duplicate Protection

Before assigning a number

SQLite shall verify uniqueness.

Duplicate numbers are prohibited.

---

# Reserved Numbers

The engine may reserve report numbers before report generation to avoid collisions during batch processing.

---

# Batch Generation

Sequential numbering is guaranteed even when generating multiple reports in one operation.

Example

```
TR-2026-000125

TR-2026-000126

TR-2026-000127
```

No gaps shall occur unless generation fails after reservation.

---

# Manual Numbering

Disabled by default.

Administrator may enable manual numbering for legacy migration only.

Every manually assigned number shall still be validated for uniqueness.

---

# Engineering Independence

The Report Numbering Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

It assigns identifiers only.

---

# SQLite Interaction

SQLite stores

Current Counter

Document Prefix

Numbering Rules

Reserved Numbers

Generated Numbers

Revision Links

Audit History

---

# Error Handling

Counter Missing

↓

Initialize

Duplicate Number

↓

Generate Next

SQLite Failure

↓

Abort

Invalid Rule

↓

Use Default

---

# Performance Targets

Generate Number

< 5 ms

Duplicate Verification

< 5 ms

Batch Reservation

< 100 ms

---

# Acceptance Criteria

✔ Unique numbering

✔ Duplicate prevention

✔ Configurable format

✔ Revision compatibility

✔ Batch numbering support

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 document control compliant

✔ Complete traceability from TXT file

---

End of Document
