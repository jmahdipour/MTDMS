# Cache Manager

Document ID : MTDMS-UTL-004

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

System Utilities

Status

Production

---

# Purpose

The Cache Manager improves application responsiveness by temporarily storing frequently accessed information in memory.

Caching is used only to improve performance.

The cache shall never replace the SQLite database as the authoritative source of information.

Engineering calculations shall always use validated data.

---

# Objectives

The Cache Manager shall

• Reduce database access

• Improve application speed

• Improve search performance

• Reduce repeated calculations

• Minimize disk access

• Automatically invalidate outdated cache

---

# Architecture

```
SQLite Database

↓

Cache Manager

↓

Memory Cache

↓

Application Modules
```

---

# Cache Categories

Material Library

Standard Library

Application Settings

Machine Configuration

Template Information

Search Index

Recently Imported Files

Frequently Used Metadata

---

# Cache Policy

Read

↓

Cache

↓

Reuse

↓

Invalidate

↓

Reload

---

# Cache Lifetime

Application Session

Default

Administrator configurable

Temporary

Permanent Session

Manual Refresh

---

# Cache Loading

Automatic

Application Startup

On Demand

First Access

Manual

Administrator Command

---

# Cache Refresh

Triggered by

Material Update

Standard Update

Configuration Change

Template Change

Database Restore

Manual Refresh

---

# Cache Invalidation

The cache shall be cleared when

Database Version Changes

Configuration Changes

Application Restart

Manual Clear

Integrity Failure

---

# Cached Objects

Each cached object contains

Object ID

Version

Timestamp

Source Table

Checksum

Expiration Status

---

# Cache Verification

Verify

Object Exists

Version Match

Checksum Match

Expiration

If verification fails

↓

Reload from SQLite

---

# Memory Management

Maximum Cache Size

Administrator configurable.

When memory limit is reached

Least Recently Used (LRU)

objects are removed first.

---

# Cache Strategy

Default

Read Through Cache

SQLite remains the master data source.

---

# Cache Statistics

Monitor

Cache Hits

Cache Misses

Reload Count

Memory Usage

Cache Size

Hit Ratio

---

# Performance Goals

Material Lookup

< 10 ms

Settings Lookup

< 5 ms

Template Lookup

< 20 ms

Search Cache

< 50 ms

---

# SQLite Database

Tables

```
tblCacheStatistics

tblCacheConfiguration
```

---

# Logging

Record

Cache Loaded

Cache Cleared

Cache Refreshed

Cache Miss

Cache Hit

Memory Warning

---

# Permissions

Administrator

Configure Cache

Quality Manager

View Statistics

Operator

No Access

---

# Error Handling

Cache Corrupted

↓

Discard

↓

Reload

Memory Full

↓

Remove Old Entries

SQLite Unavailable

↓

Use Existing Cache (Read Only)

Version Mismatch

↓

Reload

---

# Future Enhancements

Persistent Cache

Compressed Cache

Shared Cache

Cloud Cache

Predictive Cache

Reserved

---

# Acceptance Criteria

✔ Improves performance

✔ SQLite remains authoritative

✔ Automatic invalidation

✔ Memory management

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering independent

✔ Complete cache statistics

---

End of Document
