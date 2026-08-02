# EDR-001 — Unit Boundary and Conversion

- Status: FROZEN — APPROVED BY PROJECT OWNER
- Date: 2026-08-02
- Approved: 2026-08-02
- Classification: NORMATIVE
- Scope: Device import, calculation, graph, report, and audit
- Resolves: CONFLICT-UNIT-001

## Context

The current device sample supplies force in kilogram-force (`kgf`).
The Frozen engineering rule uses `kgf` and `kgf/mm²` internally, while other
production specifications require SI normalization before calculation.
Raw acquisition values must remain traceable and must never be overwritten.

## Decision

1. Every imported measurement channel shall declare an input unit.
2. The default force unit for the current device profile shall be `kgf`.
3. Raw values and raw units shall be preserved exactly as imported.
4. An unknown or ambiguous input unit shall block calculation until confirmed.
5. Operator confirmation of an inferred or selected input unit shall be audited.
6. Until a superseding Frozen EDR is approved, calculation force shall be `kgf`.
7. Until a superseding Frozen EDR is approved, calculation stress shall be `kgf/mm²`.
8. Output units shall be independently selectable for display, graph, and report.
9. Output-unit changes shall not change the underlying physical result.
10. All conversions shall use one centralized unit-conversion service.
11. Conversion factors shall not be duplicated in worksheet or engine formulas.
12. Every graph axis shall display the selected quantity and unit.
13. The audit trail shall record raw unit, calculation unit, output unit, factor,
    unit source, operator confirmation, timestamp, and profile identifier.

## Supported units

- Force: `kgf`, `N`, `kN`, `lbf`
- Stress: `kgf/mm²`, `MPa`, `GPa`, `psi`
- Displacement/extension: `mm`, `µm`, `in`
- Strain: dimensionless, `%`, `µε`
- Time: `s`, `min`
- Temperature: `°C`, `°F`, `K`

## Exact conversion constants

- `1 kgf = 9.80665 N`
- `1 kgf/mm² = 9.80665 MPa`
- `1 kN = 1000 N`
- `1 in = 25.4 mm`
- `1 lbf = 4.448221615 N`

## Required value metadata

`RawValue`, `RawUnit`, `CanonicalValue`, `CanonicalUnit`, `DisplayValue`,
`DisplayUnit`, `ConversionFactor`, `UnitSource`, and `OperatorConfirmation`.

## Compatibility and migration

This decision preserves the currently Frozen calculation path. A future EDR may
change canonical calculation units to SI without changing historical raw data.
Such a change shall define database migration, recalculation, versioning, and
backward-comparison rules before it becomes Frozen.

## Governance

This EDR was approved by the project owner on 2026-08-02 and is Frozen.
It is the latest valid EDR and supersedes conflicting unit-boundary statements
for the scope defined above. Any change requires a new, explicitly approved EDR.

Workbook construction remains blocked until the RTM is semantically consolidated
and every accepted requirement is linked to an executable acceptance test.
