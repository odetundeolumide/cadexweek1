# CadetX — Heavy Supplier, Inventory & Warehouse Analytics

## Week 1 submission: Data Profiling & Data Cleaning

## Team

- **Odetunde Olumide Temitope** — Data Scientist. Scrum Master this week.
- **Kukoyi Zainab Omotola** — Data Analyst-
- **Nyong Asuabiat** — Data Analyst

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
  with `invoice_id_ambiguous`
