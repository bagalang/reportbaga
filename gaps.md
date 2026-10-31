# reportbaga — gaps

## Closed 0.1.0

- HTML first `<table>` → CsvTable → XLSX / CSV
- `fixtures/oborotna.html` accounting-style demo
- CSV → XLSX bridge

## Open

### R1 — ~~only first table~~ — closed 2026-10-31 (XLSX multi-sheet)

`ReportMultiIR` (ir.baga): title + meta + `Vec<str>` sheet names +
`Vec<CsvTable>` tables. `report_multi_to_xlsx` (report.baga) генерира
multi-sheet XLSX: workbook с N sheet entries, rels с N rIds, sheet1..N.xml.
PDF/CSV/HTML остават single-table (first sheet).

### R2 — PDF + office from HTML

HTML (XHTML table) → PDF / XLSX / ODS / DOCX / ODT via ReportIR.

### R3 — HTML must be well-formed XHTML

Uses xmlbaga; lenient HTML5 not supported.

### R4 — ~~no number formatting~~ — closed 2026-10-31

`report_fmt_bgn(s)`: числов низ → BGN формат (запетая за десетични, nbsp
за хиляди, точно 2 десетични). `report_is_number` разпознава числа.
`report_table_to_html_fmt` — table с форматиране на числови клетки.
Freeze panes остава (вече има в xlsx пътя).
