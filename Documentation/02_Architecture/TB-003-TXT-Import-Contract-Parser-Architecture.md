# TB-003 — TXT Import Contract & Parser Architecture

**Document:** TB-003  
**Project:** MTDMS — Material Test Data Management System  
**Version:** 1.0  
**Status:** Approved / Frozen  
**Scope:** Output TXT file analysis only  
**Platform:** Excel 2019 VBA Add-in  
**Calculation model:** Array-based

---

## 1. Purpose

This document defines the contract and architecture for reading the exported TXT file, extracting the approved metadata and data section, validating the imported structure, and producing the input object for `EngineeringDataset`.

The importer performs no engineering calculations.

```text
TXT
 ↓
File Reader
 ↓
Raw Lines
 ↓
Parser
 ├── Metadata
 └── Data
 ↓
Structural Validation
 ↓
EngineeringDataset
```

No calculation engine reads the TXT file directly.

---

## 2. File Reader Contract

The File Reader is responsible for:

- opening the selected TXT file;
- reading the complete file in source order;
- preserving every source line;
- decoding the file text;
- retaining line numbers;
- closing the file safely.

The reader does not remove blank lines, normalize numeric values, repair malformed rows, or perform engineering calculations.

Runtime representation:

```text
RawLines(1)
RawLines(2)
...
RawLines(N)
```

The raw line collection remains available for traceability and audit.

---

## 3. Encoding

Encoding is a File Reader concern and must not depend silently on the Excel/Windows regional settings.

Conceptual flow:

```text
Encoding Detection / Configuration
 ↓
Decode
 ↓
RawLines
```

If the file cannot be decoded reliably, the import must stop with an encoding error.

---

## 4. Approved Metadata Contract

Only these metadata lines are authoritative in the current version:

| Line | Source field | Internal field |
|---:|---|---|
| 10 | `d/a` | `DiameterOrArea` |
| 11 | `b` | `Width` |
| 13 | `L0` | `InitialLength` |

All other metadata is ignored until separately approved.

The parser extracts values but does not infer whether `d/a` represents a diameter or an area. That interpretation belongs to specimen/configuration logic.

---

## 5. Metadata Parsing

Each approved metadata line follows this conceptual operation:

```text
Raw Line
 ↓
Trim / Locate Field
 ↓
Separate Label and Value
 ↓
Invariant Numeric Parse
 ↓
Metadata Field
```

`L0` must be numeric and greater than zero during engineering validation.

Metadata extraction must retain the original source line number for provenance.

---

## 6. Data Header Contract

The parser identifies the data section using the approved data header rather than relying only on a hard-coded starting row.

Current header:

```text
No               Time              Displacement      Deformationt      Force
```

The logical columns are:

```text
No
Time
Displacement
Deformationt
Force
```

Whitespace differences around the names must not prevent recognition.

---

## 7. Separator Contract

The current exported format is CSV-like TXT with comma separators.

```text
Separator = ","
```

The parser may isolate separator handling so a future device-format variation can be supported without changing the Dataset contract.

---

## 8. Data Row Contract

Every valid data row contains five logical values:

```text
No
Time
Displacement
Deformationt
Force
```

Example:

```text
11, 0.5, 0.020, 0, 2.03598
```

becomes:

```text
No            = 11
Time          = 0.5
Displacement  = 0.020
Deformationt  = 0
Force         = 2.03598
```

The parser preserves source order and does not calculate stress or strain.

---

## 9. Runtime Types and Units

| Field | Runtime type | Source unit |
|---|---|---|
| `No` | Long | — |
| `Time` | Double | source-file time unit |
| `Displacement` | Double | mm |
| `Deformationt` | Double | mm |
| `Force` | Double | kgf |

Force remains `kgf` in the raw Dataset. Conversion to Newton is a calculation-engine responsibility.

---

## 10. Invariant Numeric Parsing

TXT numeric syntax must be interpreted independently from Excel/Windows regional settings.

For example, a source value such as:

```text
0.012
```

must not become dependent on whether Excel expects `.` or `,` as the local decimal separator.

The parser converts valid source numeric text to `Double` only after interpreting the source format.

The parser must not use regional conversion as an implicit data-format definition.

---

## 11. Missing Values

An empty field is not zero.

```text
0       → valid numeric zero
empty   → missing
invalid → invalid
```

Example:

```text
11, 0.5, 0.020, , 2.03598
```

must preserve the missing `Deformationt` state rather than converting it to zero.

---

## 12. Point Number (`No`)

`No` is parsed as an integer value.

The importer must not reconstruct or renumber it.

If the source contains a gap:

```text
1
2
3
7
8
```

the gap is retained. Any sequence-consistency warning belongs to validation, not parsing.

---

## 13. Time

The parser stores the source Time values without filtering, smoothing, interpolation, or correction.

Monotonicity and other engineering suitability checks belong to validation.

---

## 14. Displacement

`Displacement()` is raw source data.

No smoothing, filtering, extrapolation, baseline correction, or conversion is performed by the importer.

---

## 15. Deformationt

`Deformationt` is always parsed as a raw column when present in the approved data header.

The importer does not decide whether it is a valid extensometer measurement.

For example, the column may contain changing values while an extensometer is active or zeros when it is not active.

Validity and source selection are handled by the later strain-source/event logic.

---

## 16. Force

Force is imported in the source unit:

```text
kgf
```

The parser does not convert it to Newton.

The conversion is explicitly deferred to the Calculation Pipeline.

---

## 17. Data Row Validation

For every source data row, the parser/structural validator checks:

- expected column count;
- numeric convertibility of required fields;
- integer nature of `No`;
- presence versus missing state;
- source line number;
- original text.

Invalid rows are not silently repaired.

---

## 18. Malformed Rows

Example:

```text
12, 0.7, 0.028
```

has fewer than the required five fields.

It must be marked as an invalid row and must not enter the valid calculation arrays as a fabricated row.

The importer must not fill missing fields with zero or previous values.

---

## 19. Invalid Numeric Values

Example:

```text
12, 0.7, ABC, 0, 7.12
```

must produce an issue such as:

```text
INVALID_NUMERIC_VALUE
```

with the relevant source line, column, raw value, and error information retained.

---

## 20. Import Issue Model

Conceptual structure:

```text
ImportIssue
├── Severity
├── LineNumber
├── Column
├── RawText
├── ErrorCode
└── Message
```

Severity values:

```text
INFO
WARNING
ERROR
```

Representative error codes:

```text
FILE_NOT_FOUND
FILE_ACCESS_DENIED
ENCODING_ERROR
METADATA_LINE_MISSING
METADATA_VALUE_INVALID
DATA_HEADER_NOT_FOUND
DATA_COLUMN_MISSING
DATA_ROW_INVALID
NUMERIC_VALUE_INVALID
MISSING_VALUE
```

---

## 21. End of Data

The normal data structure is:

```text
Data Header
 ↓
Data Row
 ↓
Data Row
 ↓
...
 ↓
EOF
```

If additional lines occur after data has started and cannot be interpreted as valid data rows, they must not be silently discarded.

For the MVP, such lines generate an import/validation warning or error according to their severity; raw source text remains preserved.

---

## 22. No Silent Repair

The Importer is a parser, not a repair engine.

It must never silently perform operations such as:

```text
ABC → 0
missing → previous value
missing → zero
bad row → interpolated row
bad No → regenerated No
```

Any future repair facility must be an explicit, separately auditable operation requiring operator approval.

---

## 23. Raw Preservation and Traceability

The relationship between source text and Dataset point must remain recoverable.

Conceptual mapping:

```text
PointMap(i)
├── DatasetIndex
├── SourceLineNumber
└── OriginalNo
```

Example:

```text
DatasetIndex = 1250
SourceLineNumber = 1268
OriginalNo = 1249
```

This allows a calculated result to be traced back to the exact source row.

---

## 24. ParsedFile Intermediate Object

The parser should conceptually produce:

```text
ParsedFile
├── FileInfo
├── RawLines
├── Metadata
├── RawData
├── PointMap
└── ImportIssues
```

Then:

```text
ParsedFile
 ↓
Validation
 ↓
EngineeringDataset
```

This separation prevents parser responsibilities from leaking into engineering calculations.

---

## 25. Parser Boundary

The parser must have no knowledge of:

- Young's modulus;
- yield point calculation;
- UTS;
- true stress/strain;
- Material Library;
- Secondary Length;
- Graph Correction;
- fracture interpretation;
- report formatting.

These belong to later stages.

---

## 26. Relationship to Strain Source Logic

The importer reads both:

```text
Deformationt()
Displacement()
```

but does not choose between them.

Later logic uses the independently defined events:

```text
YieldPoint
ExtensometerReleasePoint
FracturePoint
```

and creates segmented strain-source information such as:

```text
Segment 1 → EXTENSOMETER
Segment 2 → CROSSHEAD
```

Thus:

```text
Deformationt column exists
        ≠
Extensometer is active
```

---

## 27. EngineeringDataset Handoff

After successful parsing and validation, the importer hands off:

```text
FileInfo
Metadata
RawData
PointMap
Validation state
Import issues
Provenance
```

to `EngineeringDataset`.

No stress, strain, modulus, yield, fracture, or graph correction result is created by TB-003.

---

## 28. Complete Import Pipeline

```text
                 TXT
                  │
                  ▼
           File Validation
                  │
                  ▼
             File Reader
                  │
                  ▼
              RawLines()
                  │
                  ▼
          Encoding / Decode
                  │
                  ▼
           Metadata Parser
                  │
             ┌────┼────┐
             ▼    ▼    ▼
            L10  L11  L13
             │    │    │
             └────┼────┘
                  ▼
          Data Header Parser
                  │
                  ▼
            Data Row Parser
                  │
                  ▼
        Structural Validation
                  │
                  ▼
          EngineeringDataset
```

---

## 29. Approved Design Decisions

| ID | Decision |
|---|---|
| D-17 | File Reader preserves all source lines and source order. |
| D-18 | Parser reads only approved metadata lines 10, 11, and 13. |
| D-19 | Data header is identified by logical column names, not only by row number. |
| D-20 | Current separator is comma. |
| D-21 | Numeric parsing is independent of Excel/Windows regional settings. |
| D-22 | Missing values are not converted to zero. |
| D-23 | Parser never renumbers source `No` values. |
| D-24 | Raw Force remains kgf until the Calculation Engine. |
| D-25 | Parser performs no smoothing, filtering, interpolation, or engineering calculation. |
| D-26 | Invalid rows are not silently repaired. |
| D-27 | Source line-to-Dataset point mapping is retained. |
| D-28 | Parser produces a ParsedFile intermediate representation before EngineeringDataset. |
| D-29 | Parser has no knowledge of Material Library or Graph Correction. |
| D-30 | Deformationt is imported as raw data; extensometer validity/source selection is handled later. |

---

## 30. Next Blueprint

**TB-004 — Engineering Calculation Pipeline**

The next document will define the array-based calculation chain from raw `Force (kgf)` and specimen metadata through force conversion, area, stress, segmented strain source, Young's modulus, yield, UTS, fracture, true stress/strain, and post-fracture elongation, while clearly separating raw results from graph-correction results.

No application code is defined by this document.
