# UK Glass Fixing / Repair Companies (Top 50) - Research

## Research question

Identify a search-derived list of top UK companies whose **main focus is glass fixing/repair** (emergency glazing, shopfront/window/door glass repair and replacement), then map them to Companies House and extract latest available financial figures (profit/revenue where available).

## What was done

1. Collected candidate companies from multiple web searches and industry directories focused on:
   - emergency glazing
   - shopfront glass repair
   - commercial window/door glass repair and replacement
2. Applied a strict inclusion rule: company website/listing had to be repair-first (glass fixing as the main service).
3. Built a top-50 list from those search results (not an official market ranking).
4. Queried Companies House for each company name to find likely legal entities.
5. Pulled latest available machine-readable accounts data from XHTML filings where available.
6. Extracted:
   - `profit_gbp` when a profit/loss fact was machine-readable
   - `revenue_gbp` when a turnover/revenue fact was machine-readable
   - fallback `other_metric_*` (usually net assets) when profit/revenue was not available
7. If a value could not be reliably found, it is explicitly marked as: **`I don't know`**.

## Files

- `uk_glass_partition_companies_top50.csv` - main dataset (50 companies)
- `summary_stats.txt` - quick computed stats used for this summary

## Data fields (CSV)

- `rank`: Research rank position (1-50)
- `company_name`: Search/discovery trading name
- `website`: Source website used in discovery
- `focus_check`: fixed as `repair-first`
- `focus_evidence`: short note showing why company was treated as repair-first
- `companies_house_number`: matched company number (or `I don't know`)
- `companies_house_name`: matched legal entity (or `I don't know`)
- `match_confidence`: high / medium / low heuristic confidence
- `latest_accounts_period_end`: latest period seen in scanned filings
- `revenue_gbp`, `revenue_period_end`
- `profit_gbp`, `profit_period_end`
- `other_metric_label`, `other_metric_value_gbp`, `other_metric_period_end`
- `note`: caveats (e.g., low-confidence match or missing machine-readable figures)

## Summary of findings

From the strict repair-first 50-company list:

- Profit extracted: **6/50** companies (12%)
- Revenue extracted: **2/50** companies (4%)
- This means most entities did **not** expose machine-readable turnover/profit in the filings scanned, so conclusions are directional only.

### Companies with highest extracted profit

1. Roman Glass - GBP 4,080,023 (period end: 2022-11-30)
2. GG Glass and Glazing - GBP 991,972 (period end: 2025-07-31)
3. Diamond Glass - GBP 68,640 (period end: unknown in parsed context)
4. UK Glassforce - GBP 36,007 (period end: unknown in parsed context)
5. Prentice Glass - GBP -5,149 (period end: 2025-03-31)
6. Enterprise Glass - GBP -17,747 (period end: 2023-12-31)

### Average profitability (based only on available profit figures)

- Average extracted profit: **GBP 858,957.67**
- Median extracted profit: **GBP 52,323.50**

Interpretation: The gap between average and median still suggests a **skewed distribution** where a small number of larger firms lift the mean. Typical profitability for many firms in this sample appears materially lower than the average headline value.

## Important caveats

- This is a **search-derived research sample**, not a complete or audited census of the UK market.
- Inclusion was intentionally constrained to **repair-first positioning** on discovered sources.
- A strict match threshold was applied for Companies House mapping. If the legal entity was not confidently matched, it is left as `I don't know`.
- Some matches are marked low confidence and should be manually validated before use in decisions.
- Many UK private companies file abbreviated/small-company accounts with limited P&L disclosure.
- Filing periods differ by company (not all are same year), so strict like-for-like comparison is limited.
- Profit and revenue values here come from machine-readable filings only; where not available, the dataset says `I don't know`.
