# License Manager

Document ID : MTDMS-ADM-010

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

The License Manager controls software activation, licensing, authorized features and installation validation for MTDMS.

It ensures that only licensed systems may operate while preventing unauthorized modification of licensing information.

The License Manager shall never interfere with engineering calculations already stored in the database.

---

# Objectives

The License Manager shall

• Activate software

• Validate licenses

• Control enabled modules

• Prevent unauthorized installations

• Record license history

• Support future online activation

---

# License Types

Trial

Laboratory

Professional

Enterprise

Educational

Developer

Administrator configurable.

---

# Licensing Model

Machine-based

Default

Future

Network License

USB Dongle

Cloud License

Reserved

---

# License Information

License ID

Customer

Organization

Laboratory

Issue Date

Expiration Date

Version

Edition

Maximum Users

Enabled Modules

License Status

---

# Enabled Modules

Import Engine

Engineering Engine

Graph Engine

Report Engine

Administration

Calibration

Material Library

Machine Configuration

Audit

Backup

Future Modules

Administrator configurable.

---

# Activation Workflow

```
Application

↓

Read License

↓

Verify Integrity

↓

Verify Machine ID

↓

Verify Expiration

↓

Enable Modules

↓

Application Ready
```

---

# Machine Identification

The license may be bound to

Machine ID

Windows SID (optional)

Hardware Fingerprint

Administrator configurable.

---

# License Status

Valid

Expired

Suspended

Invalid

Corrupted

Trial

---

# Expiration Handling

Before Expiration

Display Warning

After Expiration

Administrator configurable

Read Only

or

Application Blocked

---

# Integrity Verification

License file shall include

Checksum

Version

Digital Signature (Future)

Corrupted licenses are rejected.

---

# Offline Operation

Default

Supported

No Internet required.

Future

Online Verification

Cloud Synchronization

Reserved

---

# License Database

SQLite

Tables

```
tblLicense

tblLicenseHistory
```

---

# Audit Trail

Record

Activation

Deactivation

License Change

Expiration

Module Change

Administrator

Computer Name

Timestamp

---

# User Permissions

Administrator

Manage License

Laboratory Manager

View License

Operator

No Access

---

# Error Handling

License Missing

↓

Restricted Mode

License Expired

↓

Warning / Lock

Machine ID Mismatch

↓

Reject

Corrupted License

↓

Reject

---

# Future Enhancements

Online Activation

Customer Portal

Subscription License

Floating License

Hardware Dongle

Reserved

---

# Acceptance Criteria

✔ Offline capable

✔ Machine-bound licensing

✔ Module-based activation

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Complete audit trail

✔ Future cloud-ready architecture

---

End of Document
