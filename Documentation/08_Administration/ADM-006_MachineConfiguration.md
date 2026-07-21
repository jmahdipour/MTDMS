# Machine Configuration

Document ID : MTDMS-ADM-006

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

The Machine Configuration module defines the hardware configuration of every testing machine connected to MTDMS.

Unlike the Equipment Manager, which stores inventory and calibration information, this module stores the technical operating configuration required by the software.

This configuration is loaded every time a machine is connected.

---

# Reference Standards

ISO/IEC 17025

ISO 7500-1

ISO 9513

ISO 6892-1

ASTM E4

ASTM E74

---

# Objectives

The Machine Configuration module shall

• Configure machine hardware

• Configure communication

• Configure measurement channels

• Configure load cells

• Configure extensometers

• Configure limits

• Prevent invalid configurations

---

# Supported Machines

Universal Testing Machine

Compression Machine

Spring Tester

Ring Stiffness Tester

Bending Tester

Impact Machine

Hardness Machine

Custom Machine

---

# Hardware Architecture

```
Testing Machine

↓

PLC

↓

Communication Driver

↓

Machine Configuration

↓

Engineering Engine
```

---

# Machine Information

Machine ID

Machine Name

Manufacturer

Model

Serial Number

Software Version

PLC Model

Communication Driver

Status

---

# Communication

Supported Types

Ethernet

USB

RS-232

RS-485

TCP/IP

Future

OPC UA

Administrator configurable.

---

# PLC Configuration

Supported PLC

FATEK

Facon

Future

Siemens

Omron

Mitsubishi

Reserved

---

# Network Settings

IP Address

Subnet Mask

Gateway

Port

Timeout

Retry Count

Heartbeat Interval

Administrator configurable.

---

# Load Cell Configuration

Each machine may contain multiple load cells.

Typical configuration

100 kg

500 kg

2 ton

10 ton

25 ton

For each load cell

Load Cell ID

Capacity

Resolution

Calibration Date

Correction Factor

Status

Default Load Cell

---

# Extensometer Configuration

Each extensometer contains

Extensometer ID

Gauge Length

Range

Resolution

Calibration Date

Correction Factor

Status

Default Extensometer

Example

10 mm

50 mm

100 mm

---

# Measurement Channels

Channel Number

Channel Name

Signal Type

Engineering Unit

Gain

Offset

Filter

Enabled

---

# Signal Types

Force

Extension

Displacement

Time

Temperature

Humidity

Pressure

Auxiliary

---

# Sampling Configuration

Sampling Rate

Maximum Frequency

Minimum Frequency

Automatic Mode

Manual Mode

Buffer Size

---

# Control Modes

Force Control

Displacement Control

Extension Control

Time Control

Load Hold

Position Hold

Administrator configurable.

---

# Safety Limits

Maximum Force

Maximum Extension

Maximum Displacement

Emergency Stop Force

Emergency Stop Extension

Travel Limits

Soft Limits

Hard Limits

---

# Motion Parameters

Approach Speed

Test Speed

Return Speed

Jog Speed

Acceleration

Deceleration

---

# Machine Capabilities

Supported Tests

Tensile

Compression

Bending

Spring

Ring Stiffness

Impact

Administrator configurable.

---

# Startup Validation

Verify Communication

↓

Verify PLC

↓

Verify Load Cells

↓

Verify Extensometer

↓

Verify Channels

↓

Ready

---

# SQLite Database

Tables

```
tblMachine

tblLoadCell

tblExtensometer

tblMachineChannel

tblCommunication
```

---

# Permissions

Administrator

Full Access

Calibration Engineer

Load Cell Configuration

Maintenance Engineer

Communication

Operator

Read Only

---

# Audit Trail

Configuration changes record

User

Date

Time

Old Value

New Value

Computer

Reason

---

# Error Handling

Communication Failure

↓

Reconnect

Load Cell Missing

↓

Block Test

Extensometer Missing

↓

Warning

Configuration Corrupted

↓

Restore Backup

Unknown PLC

↓

Abort

---

# Future Enhancements

Automatic Hardware Discovery

Auto PLC Detection

Remote Diagnostics

Cloud Configuration

Self-Test Wizard

Reserved

---

# Acceptance Criteria

✔ Supports multiple load cells

✔ Supports multiple extensometers

✔ PLC configurable

✔ Communication configurable

✔ Safety limits configurable

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

---

End of Document
