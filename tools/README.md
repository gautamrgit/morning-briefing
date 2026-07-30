# Tools

Utilities used to generate recurring deliverables. Not part of the published briefing site.

## fmcg-quarterly-tracker.html

Source template for the **India FMCG quarterly results comparison PDF**.

### What it is
A mobile-readable A5 portrait document comparing Indian FMCG companies' quarterly
results, using stacked per-company cards rather than a wide table (wide tables force
pinch-zoom on a phone).

### How to render

```
wkhtmltopdf --enable-local-file-access -s A5 -O Portrait \
  fmcg-quarterly-tracker.html output.pdf
```

Requires `wkhtmltopdf`. Fonts: DejaVu Sans / DejaVu Serif (renders the rupee glyph,
em dashes and accented characters correctly).

### Rerun procedure
1. Fetch this file from the repo (the working container does not persist between sessions).
2. Web-search each newly reported company for the quarter's numbers.
3. Add a `<div class="card">` block per new company, following the existing pattern.
4. Re-sort cards by outcome, not reporting date — expanders first, decliners last.
5. Update the "Four readings" and "Still to come" sections.
6. Re-render and deliver the PDF.

### Conventions
- `card win` = green spine (grew revenue *and* expanded margin)
- `card` = neutral spine (grew revenue, margin flat)
- `card lose` = red spine (margin contraction or revenue decline)
- `.pos` green / `.neg` red on individual values
- Calculated (not reported) figures get an asterisk and a footnote in `.note`
- `n/d` = not disclosed. Never infer a disclosed figure silently.

### Metrics tracked per company
Revenue, revenue growth, volume growth, gross margin, EBITDA/operating margin,
EBITDA growth, PAT, PAT ex-one-offs, EPS, ad spend, ad spend/sales, day-one stock move.

### Analytical frame
The recurring thesis across quarters is **ad spend direction versus revenue growth**
as a signal of management confidence:
- Ad spend growing faster than revenue = investing from strength
- Ad spend growing slower than revenue = using A&P as a margin lever
- Ad spend rising while revenue falls = share defence

Reckitt H1/FY results and P&G global results are carried as reference blocks, since
neither is on the Indian April–March reporting calendar.

### Coverage set
Reported and tracked: Nestlé India, HUL, Dabur, Colgate-Palmolive India,
P&G Hygiene & Health Care (PGHH).

Still to add: ITC, Marico, Britannia, Gillette India, GCPL, Tata Consumer, Emami,
Jyothy Labs, Honasa, Varun Beverages.

**Priority watch — GCPL.** The only remaining reporter with a household insecticides
and home care book directly comparable to Reckitt's. If GCPL repeats HUL's Home Care
pattern (strong revenue, flat segment profit), that confirms aisle-wide promotional
intensity rather than an HUL-specific execution issue.

### Note on fiscal calendars
PGHH moved from a July–June to an April–March fiscal year, so its June quarter is now
Q1 FY27 and comparable to peers. P&G globally still runs July–June — its June quarter
is Q4. Do not mix the two.
