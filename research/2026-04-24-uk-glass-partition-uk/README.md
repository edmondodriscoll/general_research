# UK Glass Repair / Glass Partition Companies (Top 50) - Research

## Research question

Identify a search-derived list of top UK companies offering glass repair and/or commercial glass partition and glass-door services, then map them to Companies House and extract latest available financial figures (profit/revenue where available).

## What was done

1. Collected candidate companies from multiple web searches and industry directory pages focused on:
   - commercial glass partitions
   - office glass doors
   - commercial glazing and repair
2. Built a top-50 list from those search results (not an official market ranking).
3. Queried Companies House for each company name to find likely legal entities.
4. Pulled latest available machine-readable accounts data from XHTML filings where available.
5. Extracted:
   - `profit_gbp` when a profit/loss fact was machine-readable
   - `revenue_gbp` when a turnover/revenue fact was machine-readable
   - fallback `other_metric_*` (usually net assets) when profit/revenue was not available
6. If a value could not be reliably found, it is explicitly marked as: **`I don't know`**.

## Files

- `uk_glass_partition_companies_top50.csv` - main dataset (50 companies)
- `summary_stats.txt` - quick computed stats used for this summary

## Data fields (CSV)

- `rank`: Research rank position (1-50)
- `company_name`: Search/discovery trading name
- `website`: Source website used in discovery
- `search_source`: Brief note of search/directory origin
- `companies_house_number`: matched company number (or `I don't know`)
- `companies_house_name`: matched legal entity (or `I don't know`)
- `match_confidence`: high / medium / low heuristic confidence
- `latest_accounts_period_end`: latest period seen in scanned filings
- `revenue_gbp`, `revenue_period_end`
- `profit_gbp`, `profit_period_end`
- `other_metric_label`, `other_metric_value_gbp`, `other_metric_period_end`
- `note`: caveats (e.g., low-confidence match or missing machine-readable figures)

## Summary of findings

From the 50-company list:

- Profit extracted: **7/50** companies (14%)
- Revenue extracted: **1/50** companies (2%)
- This means most entities did **not** expose machine-readable turnover/profit in the filings scanned, so conclusions are directional only.

### Companies with highest extracted profit

1. Aluprof - GBP 5,624,813 (period end: 2022-12-31)
2. Fusion Partitions - GBP 2,833,335 (period end: 2023-05-31)
3. Komfort Partitioning - GBP 366,720 (period end: 2024-12-31)
4. Cheadle Glass Company - GBP 115,438 (period end: 2016-05-31)
5. Clestra Hauserman - GBP 107,735 (period end: 2021-12-31)

### Average profitability (based only on available profit figures)

- Average extracted profit: **GBP 1,299,375**
- Median extracted profit: **GBP 115,438**

Interpretation: The gap between average and median suggests a **skewed distribution** where a small number of larger businesses materially raise the average. Typical profitability for many firms in this sample appears much lower than the average headline value.

## Important caveats

- This is a **search-derived research sample**, not a complete or audited census of the UK market.
- Some matches are marked low confidence and should be manually validated before use in decisions.
- Many UK private companies file abbreviated/small-company accounts with limited P&L disclosure.
- Filing periods differ by company (not all are same year), so strict like-for-like comparison is limited.
- Profit and revenue values here come from machine-readable filings only; where not available, the dataset says `I don't know`.
