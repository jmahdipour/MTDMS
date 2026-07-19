# Layout Specification

Document ID : MTDMS-UI-007

Version : 0.1.0

Platform

Microsoft Excel 2019

Ribbon XML

---

# Purpose

This document defines the physical layout of every visible worksheet.

The objective is to ensure every page has identical behavior and appearance.

---

# General Layout

Every visible worksheet follows the same structure.

```
┌──────────────────────────────────────────────────────────────┐
│ Header                                                       │
├──────────────────────────────────────────────────────────────┤
│ Ribbon                                                       │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│                 Working Area                                 │
│                                                              │
├──────────────────────────────────────────────────────────────┤
│ Status Bar                                                   │
└──────────────────────────────────────────────────────────────┘
```

---

# Header Height

60 px

---

# Status Bar Height

24 px

---

# Working Area

Maximum available workbook area.

No floating objects.

---

# Worksheet Margins

Top

12 px

Bottom

12 px

Left

12 px

Right

12 px

---

# HOME Layout

```
┌─────────────────────────────────────────────┐
│ Header                                      │
├─────────────────────────────────────────────┤
│                                             │
│  Import TXT                                 │
│                                             │
│  Recent Projects                            │
│                                             │
│  Material Library                           │
│                                             │
│  Standard Library                           │
│                                             │
│  Settings                                   │
│                                             │
└─────────────────────────────────────────────┘
```

---

# IMPORT Layout

```
┌─────────────────────────────────────────────┐
│ Header                                      │
├─────────────────────────────────────────────┤
│                                             │
│ Browse TXT                                  │
│                                             │
├─────────────────────────────────────────────┤
│ TXT Preview                                 │
├─────────────────────────────────────────────┤
│ Validation                                  │
└─────────────────────────────────────────────┘
```

---

# ANALYSIS Layout

Three-column layout

```
┌──────────────┬────────────────────┬─────────────┐
│ Project      │ Stress-Strain      │ Properties  │
│ Information  │ Graph              │             │
├──────────────┼────────────────────┼─────────────┤
│ Cursor Data  │                    │ Results     │
└──────────────┴────────────────────┴─────────────┘
```

---

# Left Panel Width

280 px

---

# Right Panel Width

300 px

---

# Center Graph

Remaining width

---

# GRAPH Layout

Graph occupies approximately

75%

of worksheet width.

Right-side engineering panel

25%

---

# REPORT Layout

```
┌─────────────────────────────────────────────┐
│ Header                                      │
├─────────────────────────────────────────────┤
│                                             │
│ Report Preview                              │
│                                             │
├─────────────────────────────────────────────┤
│ Print   PDF   Excel                         │
└─────────────────────────────────────────────┘
```

---

# Hidden Worksheets

No UI formatting required.

Only structured tables.

---

# Tables

Table headers remain fixed.

Alternating row colors.

No merged cells.

---

# Graph Area

Minimum Size

900 × 550 px

Maximum

Dynamic

---

# Button Size

Standard

110 × 32 px

Large

140 × 36 px

---

# Group Box

Rounded border

Light gray background

Internal padding

8 px

---

# Alignment Rules

Buttons

Left aligned

Tables

Centered

Graphs

Centered

Headers

Centered

---

# Freeze Panes

Visible worksheets

Enabled

Top row

Frozen

Header always visible.

---

# Zoom Level

Default

100%

Allowed

80%

100%

125%

150%

---

# Worksheet Protection

Visible sheets

Protected

Unlocked cells

Input only

Hidden sheets

VeryHidden

---

# Object Naming

Panel_Project

Panel_Graph

Panel_Result

Panel_Status

Chart_StressStrain

Table_Result

Table_RawData

---

# Responsive Rules

Resolution ≥1920

Three-column layout

Resolution 1366–1919

Adaptive column widths

Resolution <1366

Horizontal scrolling permitted

---

# Future

Dual-monitor layout

Ultra-wide optimization

High-DPI scaling

---

End of Document
