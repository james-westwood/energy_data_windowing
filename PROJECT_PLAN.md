# Energy Data Windowing — Project Plan

## Goal
Analyse the NESO historic generation mix dataset using DuckDB window functions,
following the patterns described in https://duckdb.org/2021/10/13/windowing.

## Data Source
NESO historic generation mix CSV:
https://api.neso.energy/dataset/88313ae5-94e4-4ddc-a790-593554d8c6b9/resource/f93d1835-75bc-43e5-84ad-12472b180a98/download/df_fuel_ckan.csv

> Raw data is not committed to version control — add to `.gitignore`.

---

## Steps

### 1. Environment Setup
- [x] Install `uv` (requires good WiFi — ~few MB binary)
- [x] `uv init` in project directory
- [x] `uv add duckdb`

### 2. Data Acquisition
- [ ] Download `df_fuel_ckan.csv` from NESO
- [ ] Store locally under `data/raw/`
- [ ] Add `data/` to `.gitignore`

### 3. Explore the Data
- [ ] Load CSV into DuckDB
- [ ] Inspect schema, date range, row count, distinct fuel types
- [ ] Preview first 20 rows to understand shape

### 4. Clean & Model
- [ ] Parse datetime column correctly
- [ ] Confirm units (MW / GW)
- [ ] Check for nulls and time series gaps

### 5. Window Function Analysis
- [ ] Rolling averages per fuel type (e.g. 24-hour)
- [ ] Rank fuel types by output per time period
- [ ] `LAG()` to detect ramp-up / ramp-down events
- [ ] Cumulative generation share over time

### 6. Outputs
- [ ] SQL queries saved as `.sql` files or a Python script using `duckdb` module
- [ ] Results exported to Parquet or CSV for further use

### 7. Documentation & Version Control
- [ ] Push code (not data) to https://codeberg.org/Stoke2748/energy-data-windowing
- [ ] Write `README.md` explaining the analysis
