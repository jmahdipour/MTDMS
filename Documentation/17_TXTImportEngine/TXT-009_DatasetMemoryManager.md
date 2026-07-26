# Dataset Memory Manager

Document ID : MTDMS-TXT-009

Version : 1.0

Status

Core Architecture

Platform

Excel 2019 VBA

Application

MTDMS

---

# Purpose

Dataset Memory Manager مسئول مدیریت حافظه تمامی آرایه‌های EngineeringDataset است.

هیچ Engine مجاز نیست مستقیماً آرایه جدید ایجاد یا حذف کند.

تمام عملیات حافظه از طریق این Engine انجام می‌شود.

---

# Architecture

TXT

↓

EngineeringDataset

↓

Memory Manager

↓

Calculation Engine

↓

Graph Engine

↓

Report Engine

---

# Responsibilities

Allocate Arrays

Resize Arrays

Clear Arrays

Release Arrays

Copy Arrays

Clone Dataset

Check Memory

---

# Dataset Creation

Import شروع می‌شود.

↓

Memory Manager

↓

Allocate

↓

EngineeringDataset

↓

Import

---

# Allocation

قبل از Import

```
PointCount
```

مشخص می‌شود.

سپس

```vb
ReDim Force(PointCount)

ReDim Time(PointCount)

ReDim Crosshead(PointCount)

ReDim Extensometer(PointCount)
```

همه با یک اندازه ایجاد می‌شوند.

---

# Array Synchronization

تمام آرایه‌ها باید دقیقاً طول یکسان داشته باشند.

```
Force(1000)

↓

Time(1000)

↓

Crosshead(1000)

↓

Extensometer(1000)
```

عدم تطابق

↓

Fatal Error

---

# Memory Rules

هیچ Engine مجاز نیست

```
ReDim

Erase

ReDim Preserve
```

را مستقیماً اجرا کند.

فقط

Memory Manager

---

# Dynamic Resize

در صورت نیاز

```
Old Size

↓

New Size

↓

Copy

↓

Release Old
```

---

# Clear Dataset

```
Force()

↓

0

Crosshead()

↓

0

Time()

↓

0
```

Metadata حذف نمی‌شود.

---

# Clone Dataset

برای عملیات

Graph Correction

Undo

Redo

Sensitivity Analysis

یک کپی کامل ساخته می‌شود.

```
Dataset A

↓

Clone

↓

Dataset B
```

---

# Memory Protection

Dataset فقط خواندنی نیست.

ولی

Import Engine

مالک

RawData

است.

Calculation Engine

فقط

CalculatedData

را تغییر می‌دهد.

---

# Ownership

Metadata

↓

Import Engine

RawData

↓

Import Engine

CalculatedData

↓

Calculation Engine

Flags

↓

Shared

Statistics

↓

Calculation Engine

---

# Memory Layout

```
EngineeringDataset

Metadata

Raw

PointNo()

Time()

Crosshead()

Extensometer()

Force()

Calculated

Stress()

Strain()

TrueStress()

TrueStrain()

Flags

Statistics
```

---

# Maximum Dataset

نسخه فعلی

10,000,000 Points

بدون تغییر معماری

---

# Performance

Allocate

<20 ms

Clone

<100 ms

Release

Immediate

---

# Error Handling

Allocation Failed

↓

Abort

Resize Failed

↓

Abort

Out Of Memory

↓

Abort

Array Length Mismatch

↓

Fatal Error

---

# Engineering Rule

تمام محاسبات

فقط

روی Dataset موجود در RAM انجام می‌شود.

Worksheet

هرگز منبع محاسبات نیست.

---

# Acceptance

✔ Array synchronized

✔ Memory managed

✔ Clone supported

✔ Undo Ready

✔ Fast

✔ Excel Independent

✔ SQLite Compatible

---

End Of Document
