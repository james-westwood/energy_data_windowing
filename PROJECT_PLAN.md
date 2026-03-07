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
- [x] Download `df_fuel_ckan.csv` from NESO
- [x] Store locally under `data/raw/`
- [ ] Add `data/` to `.gitignore`

### 3. Explore the Data
- [x] Load CSV into DuckDB
- [x] Inspect schema, date range, row count, distinct fuel types
- [x] Preview first 20 rows to understand shape

### 4. Clean & Model
- [x] Parse datetime column correctly (DuckDB inferred timestamp automatically)
- [x] Confirm units (MW — all fuel columns are double except HYDRO/STORAGE which are int64)
- [x] Check for nulls and time series gaps (data is clean, no issues found)

### 5. Window Function Analysis
- [x] Rolling averages per fuel type (24-hour / 48-row window)
- [x] Rank fuel types by output per year (UNPIVOT + RANK() + GROUP BY year)
- [x] `LAG()` to detect ramp-up / ramp-down events (delta per 30-min interval)
- [ ] Cumulative generation share over time

### 6. Outputs
- [ ] SQL queries saved as `.sql` files or a Python script using `duckdb` module
- [ ] Results exported to Parquet or CSV for further use

### 7. Documentation & Version Control
- [x] Push code (not data) to https://github.com/james-westwood/energy_data_windowing
- [ ] Write `README.md` explaining the analysis
