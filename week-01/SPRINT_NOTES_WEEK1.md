# Sprint Notes — Week 1

**Scrum Master this week:** Odetunde Olumide Temitope
**Sprint scope:** Data Profiling & Structure Analysis, Data Cleaning & Quality Improvement

## What was completed

- Profiled all 12 original CSVs: 605,141 rows, 134 columns total,
  0 exact duplicate rows, 0 orphaned rows across 17 foreign-key
  relationships tested. Full detail in
  `Heavy_Suppliers_Warehouse_Data_Profiling_and_Structure_Analysis.pdf`.
- Cleaned all 12 files. Full detail in `DATA_CLEANING_LOG.pdf`:
  - Converted date columns stored as text to proper dates, across 7 files.
  - Split `branches.csv`'s `warehouse_capacity` (text) into a numeric
    `warehouse_capacity_sqft` column.
  - Found that `invoice_id` and `payment_id` were not unique in the
    source data — 197 and 202 IDs respectively were each shared by two
    unrelated transactions. Added new surrogate keys (`invoice_uid`,
    `payment_uid`) and flagged every affected row with
    `invoice_id_ambiguous` so it can't be silently mistaken for a
    unique key downstream.
  - Corrected one incorrect `margin_percentage` value in
    `products.csv` (product P002: 37.3 → 60.0, to match its own
    cost/price).
  - Found a scale mismatch between `inventory_master.csv`'s
    `current_stock` and its own `max_stock`/`reorder_level`/
    `safety_stock` fields. Verified `current_stock` against
    `stock_ledger` (matches exactly) and documented the mismatch
    rather than altering any values.

## Next steps
- Move into Data Integration & Dataset Merging for Week 2.
