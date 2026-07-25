# Report Batch Generation Engine

Document ID : MTDMS-RE-014

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

The Report Batch Generation Engine automatically generates multiple engineering reports and laboratory certificates in a single operation.

The engine is designed for laboratories processing large numbers of specimens where reports must be generated consistently and efficiently.

The engine performs **no engineering calculations**.

---

# Objectives

The Report Batch Generation Engine shall

• Generate multiple reports automatically

• Generate multiple certificates

• Reduce operator workload

• Ensure consistent formatting

• Preserve engineering traceability

---

# Engineering Philosophy

TXT Files

↓

Engineering Datasets

↓

Validated Results

↓

Batch Report Engine

↓

Multiple Reports

Each report is generated independently from its validated engineering dataset.

---

# Workflow

```
Selected Test Records

↓

Validate Results

↓

Select Report Template

↓

Generate Report

↓

Generate Certificate

↓

Archive

↓

Complete
```

---

# Batch Sources

Selected Reports

Date Range

Customer

Project

Material

Batch Number

Heat Number

Test Type

Machine

Operator

Administrator configurable.

---

# Supported Batch Outputs

Engineering Reports

Laboratory Certificates

Customer Reports

Summary Reports

Comparison Reports

Administrator configurable.

---

# Batch Options

Reports Only

Certificates Only

Reports + Certificates

PDF Only

Excel Only

Administrator configurable.

---

# Naming Convention

Generated files follow the configured naming rule.

Example

```
TR-2026-00125.xlsx

TR-2026-00126.xlsx

TR-2026-00127.xlsx
```

---

# Batch Progress

The engine displays

Current Report

Completed Reports

Remaining Reports

Elapsed Time

Estimated Remaining Time

Success Count

Failure Count

---

# Failure Handling

If one report fails

↓

Log Error

↓

Continue Remaining Reports

Batch processing shall not stop unless requested.

---

# Logging

Each generated document records

Report Number

Operator

Generation Time

Template

Revision

Status

Archive ID

---

# Parallel Generation

Not supported in Excel VBA.

Reports are generated sequentially to preserve stability.

---

# Engineering Independence

The Batch Generation Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Each report is created from existing validated information.

---

# SQLite Interaction

SQLite stores

Batch Job

Generated Reports

Generation Time

Operator

Failures

Audit Trail

---

# Error Handling

Missing Template

↓

Skip Report

Missing Graph

↓

Generate Without Graph (configurable)

Validation Failure

↓

Skip Report

Database Failure

↓

Abort Batch

---

# Performance Targets

Single Report

< 1 s

100 Reports

< 2 min

100 PDFs

< 5 min

Actual performance depends on graph complexity and hardware.

---

# Acceptance Criteria

✔ Batch report generation

✔ Batch certificate generation

✔ Progress monitoring

✔ Failure recovery

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability from TXT file

---

End of Document
