# Energy Data Windowing

Exploratory analysis of the [NESO historic generation mix dataset](https://api.neso.energy/dataset/88313ae5-94e4-4ddc-a790-593554d8c6b9/resource/f93d1835-75bc-43e5-84ad-12472b180a98/download/df_fuel_ckan.csv) using DuckDB window functions.

## What this project demonstrates

- Rolling averages using `AVG() OVER (ROWS BETWEEN ... PRECEDING AND CURRENT ROW)`
- Ranking within groups using `RANK() OVER (PARTITION BY ... ORDER BY ...)`
- Offset functions: `LAG()` and `LEAD()` for detecting change between intervals
- Cumulative totals using `SUM() OVER (PARTITION BY ... ORDER BY ...)`
- Reshaping wide data with `UNPIVOT` before applying window functions

## Data

301,142 rows of 30-minute generation readings from 2009 to March 2026, covering fuel types: gas, coal, nuclear, wind, solar, biomass, hydro, imports, and storage.

**The raw CSV is not committed to version control.** Download it directly from NESO:

```
https://api.neso.energy/dataset/88313ae5-94e4-4ddc-a790-593554d8c6b9/resource/f93d1835-75bc-43e5-84ad-12472b180a98/download/df_fuel_ckan.csv
```

Place it at `data/df_fuel_ckan.csv`.

## Stack

- Python 3.12
- [DuckDB](https://duckdb.org) — all queries run in-process, no database server required
- [Polars](https://pola.rs) — DataFrame output
- Jupyter — analysis notebook
- [uv](https://docs.astral.sh/uv/) — dependency management

## Setup

```bash
uv sync
jupyter lab
```

Then open `analysis.ipynb`.

## Key findings

- Coal went from 28% of generation in 2009 to effectively zero by 2025
- Wind went from 1% in 2009 to ~30% in early 2026 (winter, high wind season)
- Gas has been the #1 fuel source every year except 2012–2014, when high gas prices pushed coal to the top
- Wind has been consistently #2 since 2020 and is within 268 MW of gas in early 2026
- Nuclear output is nearly flat interval-to-interval — the clearest baseload signal in the dataset
- Biomass appears suddenly in 2017, reflecting Drax power station's conversion from coal
