# Sports and Biometrics: Indian Summer Olympic Athletes

**CS 215 — Data Analysis and Interpretation | Group 13 | IIT Bombay**

An exploratory and regression-based study of Indian athletes at the Summer Olympic Games, focusing on how physical characteristics vary across sports and how recorded athlete weight relates to height and Olympic year.

## At a glance

- **Source:** [120 Years of Olympic History: Athletes and Results (Kaggle)](https://www.kaggle.com/datasets/heesoo37/120-years-of-olympic-history-athletes-and-results)
- **Scope:** Indian Summer Olympic participation, **1936–2016** after the project's filtering and complete height/weight requirement.
- **Cleaned sample:** **835 athlete-event records** representing **522 distinct athlete IDs**. These are not 835 independent athletes.
- **Approach:** pandas-based cleaning, sport/event archetype classification, descriptive statistics, visualization, and ordinary least-squares regression.
- **Full project report:** [Checkpoint 2 report](13.pdf) | **Presentation:** [Slides (PDF)](Sports_and_Biometrics.pdf) | [Video presentation](https://drive.google.com/file/d/1hnXB5_4VtuO93WlrKYCMuT85IFcvNlVb/view?usp=drivesdk)

## Research questions

| Question | Focus | Main techniques | Detailed documentation |
| --- | --- | --- | --- |
| **[Q1](Question-1/README.md)** | How do age, height, weight and BMI differ across functional sport archetypes, including sex-specific and Athletics sub-discipline comparisons? | Grouped descriptive statistics, histograms, boxplots, scatterplots | [Question 1 README](Question-1/README.md) |
| **[Q2](Question-2/README.md)** | Does the relationship between height and weight differ by archetype after accounting for sex? | Baseline and interaction OLS, nested-model F-test, residual diagnostics, held-out prediction intervals | [Question 2 README](Question-2/README.md) |
| **[Q3](Question-3/README.md)** | Is Olympic year associated with recorded weight after adjusting for height, sex and sport composition? | Time trends, adjusted OLS, athlete-clustered uncertainty, sensitivity analysis | [Question 3 README](Question-3/README.md) |

## Main findings

- **Q1:** The analysis retains **737 athlete–year–archetype observations**. Precision has the highest mean age (about **29.21 years**), Racket Sports the highest mean height (about **176.66 cm**), and Endurance the lowest mean weight (about **61.04 kg**). These are descriptive group comparisons, not causal effects.
- **Q2:** Height and weight are positively associated (Pearson **r ≈ 0.698** among 732 athlete-year records). On the common **727-record** modelling sample, the extended sex/archetype/height-interaction model improves in-sample **R² from ≈ 0.487 to ≈ 0.576** over the height-only model.
- **Q3:** The fitted year association is approximately **+0.71 kg per decade** in the height-adjusted baseline and **+1.00 kg per decade** after also accounting for sex and archetype, using **835 event-level records**. These estimates describe associations across observed participation records, not within-person weight gains.

See each question's report for assumptions, inferential tests, plots, and limitations.

## Repository structure

```text
.
├── README.md                         # Project overview
├── 13.pdf                            # Group 13 / Checkpoint 2 project report
├── Sports_and_Biometrics.pdf         # Presentation slides
├── videolink.md                      # Video link
├── cleaning/
│   ├── README.md                     # Cleaning workflow
│   ├── data.csv                      # Raw athlete-events source dataset
│   ├── primary_data_cleaning.ipynb
│   ├── secondary_cleaning.ipynb
│   ├── final_data.csv
│   └── data_read_to_use.csv          # Final cleaned common input
├── Question-1/
│   ├── README.md
│   ├── data_for_q1.ipynb
│   ├── classification.ipynb
│   ├── stats.ipynb
│   ├── plotting.ipynb
│   ├── q1_plots/                   # Exported figures
│   └── report.pdf
├── Question-2/
│   ├── README.md
│   ├── Q2_regression_analysiss.ipynb
│   ├── plots/                      # Exported figures
│   └── question2-report.pdf
└── Question-3/
    ├── README.md
    ├── Weight_Trends_and_Archetype_Analysis.ipynb
    ├── Regression_and_sensitivity_analysis.ipynb
    ├── Q3_Model_Comparison.csv
    ├── Q3_Final_Comparison.csv
    └── Q3_report.pdf
```

Additional intermediate CSVs and exported figures are kept in their respective folders.

## Setup

Python 3 with Jupyter is recommended. From the repository root:

```bash
python -m venv .venv
source .venv/bin/activate     # Windows PowerShell: .venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install jupyterlab numpy pandas matplotlib seaborn scipy statsmodels ipython
jupyter lab
```

No dependency lockfile is included, so exact package versions are not pinned. Open the notebooks in Jupyter and choose the environment where these packages are installed.

## Suggested workflow

1. Read [cleaning/README.md](cleaning/README.md). The cleaned CSV is already checked in; rerunning cleaning is optional.
2. For **Q1**, open notebooks in the order `data_for_q1.ipynb` → `classification.ipynb` → `stats.ipynb` / `plotting.ipynb`, with the working directory set to `Question-1/`.
3. For **Q2**, follow the file-placement instructions in [Question-2/README.md](Question-2/README.md) before running the regression notebook.
4. For **Q3**, consult [Question-3/README.md](Question-3/README.md) for the required input CSV placement and notebook execution-order caveats.

**Path note:** Several notebooks use relative CSV paths. Run each notebook with its question folder as the working directory (or adjust paths). Some notebooks expect copies of data from other folders; these are documented in their READMEs. Generated plot/output paths may differ from the already committed plot folders.

## Methodological notes

- The analysis uses **three different units of observation**: 835 event participation records for the common clean dataset and Q3; 737 athlete–year–archetype rows for Q1; 732 athlete–year records before excluding five multi-archetype records in Q2 (727 modelled rows).
- The seven functional archetypes—**Combat, Endurance, Precision, Racket Sports, Speed & Power, Team Sports, Technical / Mixed**—are project-defined classifications, not columns supplied by the original dataset.
- Missing height/weight records are excluded, so findings need not generalize to all Indian Olympic participants. Ages missing after filtering are imputed with sport-and-sex medians and an overall-median fallback.
- Repeated appearances of an athlete matter for uncertainty estimates. The study is **observational** and does not identify causal effects of sport, training or time.

## Team and attribution

Group 13: **Geetha, Manohar, Nemmadi Aakash, and Teenu**. Mentor: **Mayank Jain**. See [13.pdf](13.pdf) for complete attribution, contributions, and disclosed external/LLM assistance.

**Data attribution:** [120 Years of Olympic History: Athletes and Results](https://www.kaggle.com/datasets/heesoo37/120-years-of-olympic-history-athletes-and-results). Please consult the dataset's original terms before redistributing or reusing the underlying data. No software license is specified in this repository.
