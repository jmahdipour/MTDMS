# Engineering Dataset Specification

Document ID : MTDMS-TXT-008

Version : 1.0

Status

Core Architecture

Platform

Excel 2019 VBA

Database

SQLite

Primary Source

TXT File

Application

MTDMS

---

# Purpose

EngineeringDataset تنها منبع داده برای تمام Engine های MTDMS است.

هیچ Engine دیگری مستقیماً فایل TXT را نمی‌خواند.

---

# Engineering Rule

TXT

↓

EngineeringDataset

↓

Calculation

↓

Graph

↓

Report

↓

Archive

---

# Dataset Layers

EngineeringDataset

├── Metadata

├── RawData

├── CalculatedData

├── Flags

├── Statistics

---

# Layer 1

Metadata

فقط اطلاعات ثابت آزمون

```
DA

Width

GaugeLength
```

Type

```vb
Type TestMetadata

    DA As Double

    Width As Double

    GaugeLength As Double

End Type
```

---

# Layer 2

RawData

این قسمت مستقیماً از فایل TXT پر می‌شود.

```
PointNo()

Time()

Crosshead()

Extensometer()

Force()
```

Type

```vb
Type RawDataset

    PointCount As Long

    PointNo() As Long

    Time() As Double

    Crosshead() As Double

    Extensometer() As Double

    Force() As Double

End Type
```

---

# Layer 3

CalculatedData

در هنگام Import مقداردهی نمی‌شود.

بعداً توسط

Engineering Calculation Engine

پر می‌شود.

```
Stress()

Strain()

TrueStress()

TrueStrain()

CorrectedStrain()

YoungModulus()

```

Type

```vb
Type CalculatedDataset

    Stress() As Double

    Strain() As Double

    TrueStress() As Double

    TrueStrain() As Double

    CorrectedStrain() As Double

End Type
```

---

# Layer 4

Flags

```
ExtensometerAvailable

FractureFound

YieldFound

GraphCorrected

Imported

Validated
```

Type

```vb
Type DatasetFlags

    Imported As Boolean

    Validated As Boolean

    ExtensometerAvailable As Boolean

    FractureFound As Boolean

    YieldFound As Boolean

End Type
```

---

# Layer 5

Statistics

```
PointCount

MaximumForce

MinimumForce

MaximumExtension

MaximumCrosshead

```

این مقادیر

Engineering Result

نیستند.

فقط

Dataset Statistics

هستند.

---

# Final Dataset

```vb
Type EngineeringDataset

    Metadata As TestMetadata

    Raw As RawDataset

    Calc As CalculatedDataset

    Flags As DatasetFlags

End Type
```

---

# Array Rule

تمام داده ها باید دارای Index مشترک باشند.

```
Index 125

↓

Time(125)

↓

Crosshead(125)

↓

Extensometer(125)

↓

Force(125)

↓

Stress(125)

↓

Strain(125)

↓

Graph Point 125
```

---

# Memory Rule

تمام داده ها در RAM نگهداری می‌شوند.

هیچ محاسبه‌ای روی

Worksheet

انجام نمی‌شود.

---

# Import Rule

Import فقط

RawData

را مقداردهی می‌کند.

Calculation Engine

فقط

CalculatedData

را مقداردهی می‌کند.

---

# Graph Rule

Graph Engine

فقط

EngineeringDataset

را می‌خواند.

TXT

را هرگز نمی‌خواند.

---

# Report Rule

Report Engine

فقط

EngineeringDataset

را می‌خواند.

---

# Archive Rule

SQLite

EngineeringDataset

را ذخیره نمی‌کند.

فقط

Metadata

Audit

Result Summary

را ذخیره می‌کند.

Curve در صورت نیاز Export خواهد شد.

---

# Engineering Independence

EngineeringDataset

کاملاً مستقل از

Excel

TXT

SQLite

است.

این ساختار در آینده بدون تغییر در VB.NET نیز قابل استفاده خواهد بود.

---

# Acceptance

✔ Array Based

✔ Memory Based

✔ Excel Independent

✔ TXT Independent

✔ SQLite Compatible

✔ Engineering Calculation Ready

✔ ISO 17025 Compatible

---

End of Document
