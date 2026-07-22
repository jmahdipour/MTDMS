# Certificate Database

Document ID : MTDMS-DB-009

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

The Certificate Database stores information related to laboratory test certificates.

A certificate is the officially released laboratory document.

One certificate may reference one report.

A certificate is never created directly from imported TXT data.

The workflow is

TXT

↓

Engineering Calculation

↓

Validation

↓

Report

↓

Certificate

---

# Objectives

The Certificate Database shall

• Register issued certificates

• Preserve certificate history

• Track revisions

• Support certificate search

• Preserve release traceability

---

# Design Philosophy

TXT

↓

Engineering Report

↓

Validation

↓

Certificate

The certificate represents the approved engineering report.

The certificate never replaces the original engineering data.

---

# Table Name

tblCertificate

---

# Primary Key

CertificateID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

CertificateID

INTEGER

----------------------------

CertificateGUID

TEXT

UUID

----------------------------

ReportID

INTEGER

Foreign Key

tblReport

----------------------------

CertificateNumber

TEXT

Unique

----------------------------

CertificateRevision

TEXT

Examples

R00

R01

----------------------------

IssueDate

DATE

----------------------------

IssueTime

TIME

----------------------------

CustomerID

INTEGER

Foreign Key

tblCustomer

----------------------------

MaterialID

INTEGER

Foreign Key

tblMaterialLibrary

----------------------------

OperatorID

INTEGER

Foreign Key

tblOperator

----------------------------

ReviewerID

INTEGER

Foreign Key

tblOperator

----------------------------

ApproverID

INTEGER

Foreign Key

tblOperator

----------------------------

ReleaseStatus

TEXT

Examples

Draft

Approved

Released

Archived

Cancelled

----------------------------

ApprovalDate

DATE

Nullable

----------------------------

ApprovalTime

TIME

Nullable

----------------------------

ExcelCertificatePath

TEXT

----------------------------

PDFCertificatePath

TEXT

----------------------------

ArchiveLocation

TEXT

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

# Certificate Status

Draft

Under Review

Approved

Released

Archived

Cancelled

Released certificates

shall never be modified.

---

# Certificate Release

Only reports with

Validation Complete

Approval Complete

may become certificates.

---

# Certificate Relationships

tblCertificate

↓

1 : 1

tblReport

↓

N : 1

tblCustomer

↓

N : 1

tblOperator

↓

1 : N

tblAuditTrail

↓

1 : N

tblExportHistory

---

# Engineering Independence

Certificates

store references only.

Engineering calculations

remain

inside the engineering report.

---

# File References

Store

Excel Certificate

PDF Certificate

Archive Folder

Reference TXT

Only paths are stored.

No files are stored inside SQLite.

---

# Certificate Search

Supported

Certificate Number

Customer

Date

Material

Operator

Reviewer

Status

Standard

---

# Indexes

IX_CertificateNumber

IX_IssueDate

IX_Customer

IX_Status

IX_ReportID

---

# Constraints

CertificateNumber

UNIQUE

ReportID

UNIQUE

Approval required

before Release

---

# Audit Trail

Store

Certificate

Revision

Operator

Reviewer

Approver

Timestamp

Software Version

Computer Name

---

# Permissions

Administrator

Full Access

Quality Manager

Approve

Reviewer

Review

Operator

Draft Only

Read Only

View Only

---

# Error Handling

Duplicate Certificate Number

↓

Reject

Missing Report

↓

Abort

Missing Approval

↓

Reject

Missing Archive Location

↓

Warning

---

# Acceptance Criteria

✔ Unique certificate

✔ Linked to report

✔ Linked to original TXT

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
