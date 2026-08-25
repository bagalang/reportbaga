# reportbaga


This repository is the package. The compiler and `std` stay in the baga
language monorepo. Check this tree out as `app-product/reportbaga` there
(git submodule) so path deps and `-I app-product` keep working.

## Checkout

Inside a baga language clone:

```bash
git submodule update --init --recursive
# or, first time from a fresh baga tree without the submodule recorded:
git clone git@github.com:bagalang/reportbaga.git app-product/reportbaga
```

`sandak.toml` keeps path deps so shared packages stay in baga.
`apps/report` still depends on `../reportbaga`. `tests/report_test.baga` stays in baga.
**Счетоводни отчети:** данни / HTML5 (XHTML) → **Excel · ODS · CSV · PDF · DOCX · ODT · HTML**.  
PDF с **UTF-8 / кирилица** (вграден TTF). HTML трябва да е добре формиран XHTML с `<h1>`, `<p>` и `<table>`.

| | |
|--|--|
| **sandak** | `reportbaga` **0.3.4** |
| **Deps** | csvbaga, officebaga, pdfbaga, tplbaga, xmlbaga, bufbaga |
| **Fixtures** | `fixtures/oborotna.html`, `oborotna.tpl.html` |

## Поток

```
DB / CsvTable  ──► ReportIR ──► xlsx | ods | csv | pdf | docx | odt | html
HTML preview   ──► ReportIR ──┘
tplbaga shell  ──► HTML preview + export (таблица от данни)
```

## API

```baga
// От HTML (preview в браузър) → офис / PDF
report_from_html(html, "xlsx")
report_from_html(html, "ods")
report_from_html(html, "docx")
report_from_html_io(html, "pdf")?

// От таблица (редове от SQL)
report_from_table(title, meta, csv_table, "xlsx")
report_from_table_io(title, meta, csv_table, "pdf")?

// Шаблон + данни ({{title}} {{period}} {{firm}} {{{table}}})
let ctx: Map<str,str> = map_new()
map_set(ctx, "title", "Оборотно-салдова")
map_set(ctx, "period", "2026-01")
map_set(ctx, "firm", "Демо ООД")
report_from_template(report_default_tpl(), ctx, table, "html")
report_from_template_io(tpl, ctx, table, "pdf")?
```

## CLI

```bash
cd app-product/reportbaga && sandak build

# статичен HTML
baga -I ../.. -I .. demo.baga html-xlsx fixtures/oborotna.html /tmp/o.xlsx
baga -I ../.. -I .. demo.baga html-pdf  fixtures/oborotna.html /tmp/o.pdf

# данни в кода (sample)
baga -I ../.. -I .. demo.baga data-xlsx /tmp/d.xlsx
baga -I ../.. -I .. demo.baga data-html /tmp/d.html

# tplbaga + sample
baga -I ../.. -I .. demo.baga tpl-html /tmp/t.html
baga -I ../.. -I .. demo.baga tpl-pdf  /tmp/t.pdf
```

**Product CLI:** `apps/report` — see `docs/runbooks/report.md`.  
Excel: frozen header + sheet name = report title.

## License

[MIT](LICENSE) — Copyright (c) 2026 Dim Gigov.
