# Engineering Statistical Analysis Engine

Document ID : MTDMS-CE-019

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

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

The Engineering Statistical Analysis Engine performs statistical analysis on validated engineering results that have been generated from imported TXT files.

This engine is intended for laboratory quality control, process monitoring, capability analysis, and long-term trend evaluation.

It does **not** perform engineering calculations.

It analyzes completed engineering results only.

---

# Objectives

The Statistical Analysis Engine shall

• Calculate statistical parameters

• Compare historical results

• Detect abnormal values

• Generate statistical reports

• Support laboratory quality monitoring

---

# Engineering Philosophy

TXT File

↓

Engineering Calculation

↓

Validation

↓

Engineering Results

↓

Statistical Analysis

Statistics are performed only after engineering validation.

---

# Data Sources

Validated Engineering Results

Material Library

Customer

Machine

Operator

Date Range

Standard

Batch Number

Heat Number

Production Lot

Administrator configurable.

---

# Statistical Parameters

Arithmetic Mean

Median

Minimum

Maximum

Range

Variance

Standard Deviation

Coefficient of Variation

Population Size

Sample Size

---

# Distribution Analysis

The engine shall support

Normal Distribution

Histogram

Frequency Distribution

Trend Analysis

Future capability extensions may include Weibull and Log-Normal distributions.

---

# Outlier Detection

Supported methods

3 Sigma

Interquartile Range (IQR)

User Threshold

Administrator configurable.

Outliers are flagged.

They are never deleted automatically.

---

# Historical Comparison

The engine may compare

Current Test

Previous Tests

Material Batch

Customer History

Machine History

Operator History

Date Range

---

# Trend Analysis

Supported

Strength Trend

Young's Modulus Trend

Yield Strength Trend

Spring Constant Trend

Ring Stiffness Trend

Machine Stability

Laboratory Stability

---

# Graph Output

The engine supplies

Trend Charts

Histograms

Control Charts

Distribution Curves

Comparison Charts

for later visualization.

---

# Engineering Independence

The Statistical Analysis Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Statistics are generated from copies of validated data.

---

# SQLite Interaction

SQLite stores

Statistical Results

Trend History

Control Chart Parameters

Analysis History

Audit Information

Engineering data remain unchanged.

---

# Error Handling

Insufficient Samples

↓

Warning

Missing Results

↓

Ignore

Invalid Date Range

↓

Reject

No Historical Data

↓

Information

---

# Performance Targets

Typical Dataset

100 Results

< 200 ms

1,000 Results

< 1 s

10,000 Results

< 5 s

---

# Acceptance Criteria

✔ Statistical parameters calculated

✔ Outlier detection supported

✔ Historical comparison supported

✔ Trend analysis supported

✔ Graph dataset generated

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
