# CadetX — Heavy Supplier, Inventory & Warehouse Analytics

## Week 1 submission: Data Profiling & Data Cleaning

This package contains the verified Week 1 deliverables, pulled directly
from the team's Google Drive project folder
(`HEAVY_SUPPLIERS_WAREHOUSE PROJECT`).

## Team

- **Odetunde Olumide Temitope** — Data Scientist. Scrum Master this week.
- **Teammate** — Data Analyst. (Name not yet confirmed in any shared
  document; her uploads to Drive are tied to the email
  `kukoyiomotola249@gmail.com`.)

## What's in this package

```
week-01/
├── docs/
│   ├── Heavy_Suppliers_Warehouse_Data_Profiling_and_Structure_Analysis.pdf
│   └── DATA_CLEANING_LOG.pdf
├── data/
│   └── cleaned/
│       ├── branches_clean.csv
│       ├── customers_clean.csv
│       ├── suppliers_clean.csv
│       ├── products_clean.csv
│       ├── inventory_master_clean.csv
│       ├── purchase_orders_header_clean.csv
│       ├── purchase_orders_lines_clean.csv
│       ├── sales_orders_header_clean.csv
│       ├── sales_orders_lines_clean.csv
│       ├── invoices_clean.csv
│       ├── payments_clean.csv
│       └── stock_ledger_clean.csv
├── README.md
└── SPRINT_NOTES_WEEK1.md
```

## 1. Data Profiling & Structure Analysis

Full column-level profile of the 12 original CSVs: 605,141 rows,
134 columns total, 0 exact duplicate rows, 17 foreign-key
relationships tested with 0 orphaned rows. Full detail in
`docs/Heavy_Suppliers_Warehouse_Data_Profiling_and_Structure_Analysis.pdf`.

## 2. Data Cleaning & Quality Improvement

Full detail in `docs/DATA_CLEANING_LOG.pdf`. Summary of what changed:

- Date columns converted from text to proper dates across 7 files.
- `branches.csv`: `warehouse_capacity` (text) split into
  `warehouse_capacity_sqft` (number).
- `invoices.csv` / `payments.csv`: `invoice_id` and `payment_id` were
  found to not be unique in the source data (197 and 202 IDs each
  shared by two unrelated transactions). Fixed with new surrogate
  keys `invoice_uid` / `payment_uid`, and flagged every affected row
  with `invoice_id_ambiguous`.
- `products.csv`: one incorrect `margin_percentage` value (product
  P002) corrected from 37.3 to 60.0 to match its own cost/price.
- `inventory_master.csv`: a scale mismatch between `current_stock`
  and its own `max_stock`/`reorder_level`/`safety_stock` fields was
  found, verified against `stock_ledger`, and documented — not
  altered.

## Resolved during assembly of this package

`inventory_master_clean.csv` was found to contain an extra `ratio`
column (`current_stock / max_stock`) that was not mentioned anywhere
in `DATA_CLEANING_LOG.pdf` or in the original raw file. Since it was
undocumented and easily recomputed from the two columns it derives
from, it was removed from both `data/cleaned/inventory_master_clean.csv`
in this package and the corresponding file in the Merged datasets
folder on Drive. If this column was added intentionally for a reason
not yet written down, flag it and it can be re-added with proper
documentation.
