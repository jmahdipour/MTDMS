# Email Delivery Engine

Document ID : MTDMS-RE-021

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

The Email Delivery Engine automatically sends approved engineering reports and laboratory certificates to customers and authorized recipients through email.

Email transmission is performed only after successful report approval and document generation.

The engine performs **no engineering calculations**.

---

# Objectives

The Email Delivery Engine shall

• Deliver approved reports by email

• Support multiple recipients

• Support attachments

• Record delivery history

• Maintain engineering traceability

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Validated Results

↓

Approved Report

↓

Email Engine

↓

Customer

Engineering values remain unchanged.

The engine distributes documents only.

---

# Workflow

```
Approved Report

↓

Create Email

↓

Attach Documents

↓

Send

↓

Log Result
```

---

# Email Recipients

Primary Customer

Secondary Customer

Internal Laboratory

Quality Department

Sales Department

Project Manager

Administrator configurable.

---

# Attachments

Supported

Engineering Report (PDF)

Engineering Report (Excel)

Laboratory Certificate

Graphs (optional)

CSV Export (optional)

Original TXT File (optional)

Administrator configurable.

---

# Email Subject

Default example

```
Engineering Test Report

TR-2026-00125
```

Administrator configurable.

---

# Email Body

The email body supports

Laboratory Information

Project Information

Report Number

Certificate Number

Summary

Confidentiality Notice

Administrator configurable.

---

# Supported Languages

English

Persian

Arabic

French

German

Administrator configurable.

The language follows the customer's preferred language profile.

---

# Delivery Status

Queued

Sending

Delivered

Failed

Cancelled

Resent

Administrator configurable.

---

# Delivery History

Each email records

Recipient

Date

Time

Operator

Report Number

Attachments

Delivery Result

---

# Security

Optional

Encrypted Attachment

Password Protected PDF

Digital Signature (future)

Administrator configurable.

---

# Retry Policy

Failed deliveries may be retried automatically according to administrator-defined rules.

---

# Engineering Independence

The Email Delivery Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Reports

Certificates

It distributes existing approved documents only.

---

# SQLite Interaction

SQLite stores

Recipient Profiles

Email History

Delivery Status

Retry History

Audit Trail

---

# Error Handling

Recipient Missing

↓

Reject

SMTP Failure

↓

Retry

Attachment Missing

↓

Abort

Unauthorized Report

↓

Reject

---

# Performance Targets

Single Email

< 5 s

Batch Email

Depends on SMTP Server

Attachment Preparation

< 500 ms

---

# Acceptance Criteria

✔ Automatic email delivery

✔ Multiple recipients

✔ Multiple attachments

✔ Delivery history

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability from TXT file

---

End of Document
