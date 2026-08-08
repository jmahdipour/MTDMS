# EDR-002 — Output File Only Boundary

Document ID: MTDMS-EDR-002
Version: 1.0
Status: Approved / Frozen
Date: 2026-08-08

## Decision

MTDMS is strictly an **output-file analysis system**.

The project processes only the TXT file exported by the testing machine. The software does not control, communicate with, or acquire data from the testing machine.

## In Scope

- Read-only TXT import
- Parsing the defined metadata fields
- Parsing the exported data section
- Array-based engineering calculations
- Stress/strain analysis
- Regression and Young's modulus analysis
- Yield analysis
- Fracture analysis
- Graph analysis and operator verification/correction
- Engineering reporting
- Persistent storage of metadata, results, provenance and audit information
- External curve archive referenced from SQLite

## Current TXT Contract

Only these metadata fields are currently authoritative:

- Line 10: `d/a`
- Line 11: `b`
- Line 13: `L0`

All other metadata fields are ignored until explicitly approved.

The data section currently contains:

- `No`
- `Time`
- `Displacement`
- `Deformationt`
- `Force`

Force is expressed in `kgf`.

`Deformationt` is populated when the extensometer is connected; an empty/zero signal must not be interpreted as a valid extensometer measurement without the approved source-selection rules.

## Strain Source Rule

The default strain source is Crosshead/Displacement.

The operator may manually switch the source to Extensometer.

Automatic source switching is not part of the current scope.

## Processing Rule

All engineering calculations are array-based and performed on the imported dataset in memory.

The original TXT file is immutable and is never modified.

## Explicitly Out of Scope

- PLC communication
- Fatek/Facon communication
- Machine control
- Servo/drive control
- Real-time acquisition
- Load-cell communication
- Extensometer control
- Commands sent to the testing machine
- Hardware integration

## Governance

This decision supersedes any earlier architectural wording that could be interpreted as including machine control or real-time acquisition.

Any future expansion beyond output-file analysis requires a new approved engineering decision record.
