# Question 3 — Olympic-Year Weight Trends and Sensitivity Analysis

[← Project overview](../README.md) · [Full Q3 report](Q3_report.pdf)

## Research question

**Is Olympic year associated with the recorded body weight of Indian Summer Olympic athletes after adjusting for height, and does the relationship persist when sex and sport-archetype composition are included?**

## Models and approach

1. Summarize mean weights across Olympic years and compare the changing distribution of functional sport archetypes.
2. Fit **Model A:** `Weight ~ Height + Year_Decade` (a decade-scaled year variable).
3. Fit **Model B:** `Weight ~ Height + Year_Decade + Sex + Archetype` to adjust for participation composition.
4. Examine model fit, residual diagnostics and sensitivity checks, including a **men's hockey** subset.
5. Account for repeated appearances in statistical inference using **standard errors clustered by athlete ID** where implemented in the final analysis.

## Data and main findings

The Q3 analysis uses **835 athlete-event records**, not one record per athlete or one per athlete-year. Observations span **1936–2016** and some athletes/events are represented repeatedly.

| Comparison | Estimated Olympic-year association | In-sample R² | Observations |
| --- | ---: | ---: | ---: |
| Model A: height + year | **+0.714 kg/decade** | 0.484 | 835 |
| Model B: + sex + archetype | **+0.999 kg/decade** | 0.553 | 835 |
| Men's hockey sensitivity check | **+1.312 kg/decade** | 0.456 | 198 |

Values are from `Q3_Final_Comparison.csv`; refer to the report for model-specific statistical tests and uncertainty. The positive year coefficients show *associations across the observed samples*, **not individual athletes becoming heavier over time** and not proof of a causal effect of modernization, training or nutrition.

## Files and outputs

| File | Role |
| --- | --- |
| `Weight_Trends_and_Archetype_Analysis.ipynb` | Exploratory trends, BMI, sport/event archetype assignment and descriptive analysis |
| `Regression_and_sensitivity_analysis.ipynb` | Models A/B, comparisons, visualizations and sensitivity analysis |
| `data_got_to_be_true.csv` | Cleaned data copy provided in this folder |
| `Phase2_Descriptive_Statistics.csv` | Saved descriptive summary |
| `Q3_Model_Data.csv`, `Q3_Regression_Data.csv` | Prepared regression tables |
| `Q3_Model_Comparison.csv`, `Q3_Final_Comparison.csv` | Model coefficient/fit comparisons |
| `Q3_Visualizations.pdf` | Exported visualizations |
| `Q3_report.pdf` | Full analytical report |

## Run locally

Both analysis notebooks contain relative paths referencing **`data_read_to_use.csv`**. To make this input available, start from the repository root:

```bash
cp cleaning/data_read_to_use.csv Question-3/data_read_to_use.csv
cd Question-3
jupyter lab
```

The `data_got_to_be_true.csv` file is also included, but it has a **different filename** from the one referenced by the notebooks. Run `Weight_Trends_and_Archetype_Analysis.ipynb` and then `Regression_and_sensitivity_analysis.ipynb`, using fresh kernels and checking the execution order carefully.

**Important execution caveat:** These are exploratory/annotated notebooks. A few cells refer to objects/functions defined later, or to state from previous execution. Read the accompanying Markdown notes and run prerequisite definition cells before dependent cells; a single unconditional “Run All” may fail. The checked-in result CSVs and report provide the finalized analysis even if you do not rerun notebooks.

## Interpretation cautions

- Different sports and events are represented unequally over time, and event-level records give more weight to athletes who appear in more events.
- Sport archetypes are constructed analytic groups, not naturally randomized assignments.
- Filtering to records with observed height/weight can affect representativeness.
- An adjusted time coefficient cannot on its own distinguish changing athlete selection, measurement patterns and genuine secular physical change.

Read [Q3_report.pdf](Q3_report.pdf) for plots, model assumptions and the full discussion.
