# Data Cleaning and Preparation

[← Project overview](../README.md)

This folder turns the original athlete-events dataset into the cleaned Indian Summer Olympic data used by Questions 1–3.

## Input and outputs

| File | Purpose |
| --- | --- |
| `data.csv` | Original athlete-event data supplied with the repository |
| `final_data.csv` | Intermediate filtered dataset after primary cleaning |
| `data_read_to_use.csv` | Cleaned common analysis input (835 event-level records) |
| `df_info.txt`, `data_summary.txt` | Recorded schema and summary diagnostics |
| `pandas_practice.ipynb` | Separate pandas learning/practice notebook; not required for the production cleaning pipeline |

## Pipeline

**1. `primary_data_cleaning.ipynb`**

- Read `data.csv`.
- Retain `Season == "Summer"` and `NOC == "IND"`.
- Drop exact duplicates and records missing `Height` or `Weight`.
- Sort by athlete ID and year and export `final_data.csv`.

**2. `secondary_cleaning.ipynb`**

- Read `final_data.csv`.
- Fill missing `Age` with the median within `(Sport, Sex)`, falling back to the overall median.
- Replace missing medal values with `No Medal`, remove redundant sport prefixes from `Event`, and standardize the team label.
- Drop constant/redundant columns, create `Clean_Name`, export diagnostics and `data_read_to_use.csv`.

## Reproduce

Open Jupyter with `cleaning/` as the working directory, run `primary_data_cleaning.ipynb` from top to bottom, then `secondary_cleaning.ipynb`. The checked-in output can also be used directly without regenerating it.

The analysis sample excludes athletes with missing anthropometric measurements and contains repeated event/edition appearances for some athletes. Its `ID` column identifies athletes; rows are not unique individuals.
