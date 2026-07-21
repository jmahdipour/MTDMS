# Equipment Manager

Document ID : MTDMS-ADM-005

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Administration

Status

Production

---

# Purpose

The Equipment Manager controls all laboratory equipment registered within MTDMS.

It provides complete lifecycle management, calibration traceability, maintenance history and configuration control for every measuring device used by the laboratory.

The Equipment Manager is one of the core ISO/IEC 17025 traceability modules.

---

# Reference Standards

ISO/IEC 17025

ISO 10012

ISO 7500-1

ISO 9513

ISO 376

ASTM E4

ASTM E74

---

# Objectives

The Equipment Manager shall

• Register laboratory equipment

• Track calibration status

• Track maintenance history

• Track repairs

• Assign equipment to tests

• Prevent expired equipment from use

• Maintain complete audit trail

---

# Equipment Categories

Universal Testing Machine

Load Cell

Extensometer

Hardness Tester

Impact Tester

Quantometer

Micrometer

Caliper

Dial Gauge

Thickness Gauge

Spring Tester

Temperature Sensor

Humidity Sensor

Balance

Custom Equipment

---

# Equipment Lifecycle

Purchase

↓

Registration

↓

Commissioning

↓

Calibration

↓

Routine Use

↓

Maintenance

↓

Repair

↓

Calibration

↓

Retirement

↓

Archive

---

# Equipment Information

Equipment ID

Equipment Name

Manufacturer

Model

Serial Number

Inventory Number

Software Version

PLC Version

Firmware Version

Location

Department

Status

---

# Equipment Status

Available

In Service

Under Calibration

Under Repair

Out of Service

Retired

Archived

---

# Identification

Each equipment item receives

Unique Equipment ID

Barcode

QR Code

Optional RFID

Administrator configurable.

---

# Measurement Information

Measurement Range

Resolution

Accuracy

Uncertainty

Maximum Capacity

Minimum Capacity

Engineering Units

---

# Calibration Information

Calibration Date

Due Date

Calibration Interval

Calibration Laboratory

Certificate Number

Reference Standard

Status

---

# Maintenance Information

Maintenance Date

Maintenance Type

Performed By

Description

Parts Replaced

Downtime

Next Maintenance

---

# Repair History

Repair Date

Problem Description

Corrective Action

Replacement Parts

Engineer

Repair Cost

Return to Service Date

---

# Assignment

Equipment may be assigned to

Mechanical Laboratory

Chemical Laboratory

Calibration Laboratory

Quality Control

Multiple departments supported.

---

# Equipment Usage

Each test stores

Machine ID

Load Cell ID

Extensometer ID

Software Version

Calibration Revision

This guarantees complete traceability.

---

# Search

Equipment ID

Manufacturer

Model

Serial Number

Status

Calibration Due

Department

Location

---

# Notifications

Calibration Due

30 Days Before

↓

Warning

Calibration Expired

↓

Block Use

Maintenance Due

↓

Warning

Administrator configurable.

---

# Database

SQLite

Tables

```
tblEquipment

tblEquipmentCalibration

tblEquipmentMaintenance

tblEquipmentRepair

tblEquipmentAssignment
```

---

# Audit Trail

All modifications record

User

Date

Time

Old Value

New Value

Reason

Computer Name

---

# Permissions

Administrator

Full Access

Calibration Engineer

Calibration

Maintenance Engineer

Maintenance

Operator

Read Only

Reviewer

Read Only

---

# Validation Rules

Equipment ID

Required

Serial Number

Required

Calibration Interval

Required

Duplicate Serial Numbers

Not Allowed

---

# Error Handling

Duplicate Equipment ID

↓

Reject

Expired Calibration

↓

Block Test

Missing Calibration Record

↓

Warning

Corrupted Record

↓

Restore Previous Version

---

# Future Enhancements

Automatic Calibration Scheduling

RFID Equipment Tracking

IoT Equipment Monitoring

Predictive Maintenance

Cloud Equipment Registry

Reserved

---

# Acceptance Criteria

✔ ISO/IEC 17025 compliant

✔ Complete equipment lifecycle

✔ Calibration traceability

✔ Maintenance history

✔ Repair history

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Full audit trail

---

End of Document
