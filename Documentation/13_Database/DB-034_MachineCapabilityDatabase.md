# Machine Capability Database

Document ID : MTDMS-DB-034

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Application

MTDMS

Status

Production

---

# Purpose

The Machine Capability Database stores the technical capabilities and limitations of every testing machine supported by MTDMS.

It is a **reference database**.

It does not communicate with the testing machine.

It does not modify engineering calculations.

It is used for

automatic validation

operator guidance

configuration

report information.

---

# Objectives

The Machine Capability Database shall

• Store machine capabilities

• Store available load cells

• Store extensometer information

• Store test limitations

• Support automatic validation

---

# Design Philosophy

TXT File

↓

Imported Machine

↓

Machine Capability

↓

Validation

↓

Engineering Calculation

The imported TXT file determines

what actually happened.

The Machine Capability Database defines

what the machine is capable of.

---

# Table Name

tblMachineCapability

---

# Primary Key

CapabilityID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

CapabilityID

INTEGER

----------------------------

MachineID

INTEGER

Foreign Key

tblMachine

----------------------------

CapabilityCode

TEXT

Unique

----------------------------

MaximumForce

REAL

kN

----------------------------

MinimumForce

REAL

kN

----------------------------

MaximumDisplacement

REAL

mm

----------------------------

MaximumStroke

REAL

mm

----------------------------

MaximumSpeed

REAL

mm/min

----------------------------

MinimumSpeed

REAL

mm/min

----------------------------

SupportsExtensometer

BOOLEAN

----------------------------

MaximumExtensometerTravel

REAL

mm

----------------------------

SupportsAutomaticYield

BOOLEAN

----------------------------

SupportsManualYield

BOOLEAN

----------------------------

SupportsGraphCorrection

BOOLEAN

----------------------------

SupportsCompression

BOOLEAN

----------------------------

SupportsTension

BOOLEAN

----------------------------

SupportsBending

BOOLEAN

----------------------------

SupportsSpringTest

BOOLEAN

----------------------------

SupportsRingStiffness

BOOLEAN

----------------------------

SupportsCustomTest

BOOLEAN

----------------------------

PLCModel

TEXT

Nullable

----------------------------

CommunicationType

TEXT

Examples

Ethernet

USB

Serial

----------------------------

Remarks

TEXT

Nullable

----------------------------

CreatedDate

DATE

----------------------------

ModifiedDate

DATE

----------------------------

ModifiedBy

TEXT

---

# Load Cell Support

One machine

may support

multiple load cells.

Example

100 kg

500 kg

2 ton

10 ton

25 ton

The currently selected load cell

is stored separately

inside

Machine Configuration.

---

# Extensometer Support

Multiple extensometers

may exist.

Examples

10 mm

50 mm

100 mm

The active extensometer

is selected

during testing.

---

# Engineering Independence

Machine Capability

shall never modify

Imported TXT

Engineering Results

Validation Results

Graphs

Reports

Capabilities are reference information only.

---

# SQLite Relationships

tblMachineCapability

↓

N : 1

tblMachine

↓

Referenced by

Validation Engine

Calculation Engine

Report Engine

---

# Indexes

IX_MachineID

IX_CapabilityCode

---

# Constraints

MachineID

Required

CapabilityCode

UNIQUE

MaximumForce

Required

---

# Audit Trail

Store

Machine

Capability

Old Value

New Value

Operator

Timestamp

Computer

Software Version

---

# Permissions

Administrator

Modify

Quality Manager

Modify

Reviewer

Read

Operator

Read Only

---

# Error Handling

Unknown Machine

↓

Abort

Capability Missing

↓

Warning

Invalid Force Range

↓

Reject

Duplicate Capability

↓

Reject

---

# Acceptance Criteria

✔ Machine capability stored

✔ Multiple load cells supported

✔ Multiple extensometers supported

✔ Validation support

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
