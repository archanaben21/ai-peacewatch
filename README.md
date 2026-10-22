# 🌍 AI PeaceWatch
## Conflict Early-Warning Research Using Machine Learning

**Research area:** Artificial Intelligence · Conflict Analysis · Data Science · Explainable AI  
**SDG alignment:** United Nations Sustainable Development Goal 16 — Peace, Justice and Strong Institutions  
**Project status:** Research design and proposed implementation

---

## 1. Overview

AI PeaceWatch is a proposed research project investigating whether historical conflict records and socioeconomic indicators can help estimate the likelihood of conflict in the following year.

The project aims to develop a transparent, reproducible analytical pipeline that combines public datasets, statistical analysis, machine learning and visualisation.

The initial experiment will investigate country-level conflict outcomes using historical data. It will compare simple statistical baselines with selected machine-learning models and evaluate their performance on later, previously unseen years.

The long-term vision is to explore an explainable, data-driven decision-support platform that helps researchers and relevant organisations investigate patterns associated with peace, conflict and institutional stability.

**AI PeaceWatch is not designed to predict wars with certainty.** Its purpose is to investigate whether historical data can support useful early-warning analysis, while communicating uncertainty, limitations and potential risks.

## 2. Research Question

**Can historical conflict records and selected socioeconomic indicators improve the prediction of whether a country will experience a qualifying conflict event in the following calendar year?**

### Research objectives

1. Identify suitable public datasets for historical conflict analysis.
2. Construct a consistent country-year analytical dataset.
3. Investigate relationships between historical conflict patterns and socioeconomic indicators.
4. Compare statistical baselines with machine-learning models.
5. Evaluate predictive performance using chronological validation.
6. Investigate false alarms, missed events, calibration and geographic differences.
7. Develop clear visualisations that communicate findings and uncertainty.

### Research hypothesis

A model combining lagged conflict history with selected socioeconomic indicators may outperform a simple historical-prevalence baseline on future-year observations.

This is a hypothesis to test, not an established result.

## 3. Initial Experiment

**Experiment 01: Country-Level, One-Year-Ahead Conflict Risk**

The first experiment will use country-year observations to investigate whether information available in year *t* can help estimate a defined conflict outcome in year *t + 1*.

| Component | Proposed design |
|---|---|
| Unit of analysis | Country-year |
| Forecast horizon | One calendar year |
| Prediction target | Binary indicator of a defined conflict outcome in the following year |
| Primary data source | UCDP/PRIO Armed Conflict Dataset |
| Additional data | Selected World Bank socioeconomic indicators |
| Baseline | Historical outcome prevalence |
| Initial model | Logistic regression |
| Candidate model | Random forest |
| Advanced comparison | XGBoost, if justified |
| Evaluation | Chronological holdout and rolling-origin evaluation |
| Visualisation | Historical trends, geographic maps and model evaluation plots |

The precise conflict definition, observation period, predictors and evaluation dates will be documented before model training.

An important design choice is whether the target represents any qualifying conflict in the following year or the onset of a new conflict. These are different research questions and require different outcome definitions.

## 4. Data Sources

The following sources are candidates for the initial study. Their definitions, versions, access conditions and licensing must be checked before use.

### 4.1 UCDP/PRIO Armed Conflict Dataset

**Source:** https://ucdp.uu.se/downloads/

Potential uses:

- Define a documented armed-conflict outcome.
- Examine historical conflict patterns.
- Construct country-year outcome labels.
- Derive historical conflict features where appropriate.

The selected dataset version and codebook will determine the actual variables and available years.

### 4.2 World Bank Indicators

**Source:** https://data.worldbank.org/  
**API documentation:** https://datahelpdesk.worldbank.org/knowledgebase/articles/889392-api-basic-call-structures

Potential predictors include:

- GDP growth.
- Inflation.
- Unemployment, where sufficiently comparable.
- Other theoretically justified socioeconomic indicators.

Not every indicator is available for every country and year. Missing data, publication delays and changes in measurement must be considered.

### 4.3 Optional future source: ACLED

**Source:** https://acleddata.com/

ACLED provides political-violence and demonstration-event data that may support future event-level or geographic extensions. Access conditions and permitted uses must be verified before integration.

The initial experiment will prioritise a manageable number of well-documented datasets instead of combining many sources prematurely.

## 5. Proposed Technology Stack

| Component | Tools | Purpose |
|---|---|---|
| Programming | Python | Data processing and modelling |
| Data manipulation | Pandas | Cleaning and transforming datasets |
| Research environment | Jupyter Notebook | Exploratory analysis and experiments |
| Statistical analysis | SciPy, statsmodels | Statistical relationships and baselines |
| Machine learning | Scikit-learn | Model training and evaluation |
| Advanced modelling | XGBoost | Optional boosted-tree comparison |
| Explainable AI | SHAP | Investigating model feature contributions |
| Data visualisation | Matplotlib, Plotly | Charts and interactive figures |
| Geographic analysis | GeoPandas | Geographic data processing |
| Interactive maps | Folium or Plotly | Exploring geographic patterns |
| Version control | Git, GitHub | Reproducible development and collaboration |

### Recommended initial tools

Start with:

- Python
- Pandas
- Jupyter Notebook
- Scikit-learn
- Matplotlib and Plotly
- Git and GitHub

PostgreSQL, PostGIS, FastAPI, cloud services and workflow orchestration can be introduced if later stages require them.

## 6. Research Methodology

### Step 1 — Data acquisition and audit

Download the selected conflict dataset and codebook. Retrieve a small number of socioeconomic indicators.

Document:

- Data source and version.
- Geographic coverage.
- Observation period.
- Variable definitions.
- Missing values.
- Country identifiers.
- Publication dates and licensing conditions.

### Step 2 — Country-year panel construction

Create a consistent dataset where each row represents one country and year.

Potential fields include:

- Country identifier.
- Year.
- Historical conflict status.
- Historical conflict frequency, where supported by the data.
- Lagged socioeconomic indicators.
- Defined outcome in the following year.

The final schema will depend on the selected sources.

### Step 3 — Feature engineering

Use only predictors that would have been available at the intended forecast date.

Potential features include lagged conflict history, rolling historical counts and selected socioeconomic indicators.

Avoid using future information, post-event measurements or variables derived from the target itself.

### Step 4 — Baseline modelling

Establish a simple historical-prevalence baseline and logistic regression before testing more complex models.

Add random forest and, if useful, XGBoost as subsequent comparisons.

### Step 5 — Temporal validation

Split the data chronologically into training, validation and test periods.

Use the training period to fit models, validation data to choose model settings and thresholds, and the held-out test period for final evaluation.

Rolling-origin evaluation can assess whether results remain reasonably stable across multiple historical periods.

A temporal split evaluates future-year performance for the sampled countries; it does not automatically demonstrate generalisation to countries absent from training.

### Step 6 — Interpretation and reporting

Report performance against baselines, investigate model errors and document uncertainty.

If the models do not outperform the baseline, report that result rather than presenting the system as a successful predictor.

## 7. Model Evaluation

Accuracy alone is insufficient, particularly when conflict outcomes are uncommon.

Depending on the final research design, evaluation may include:

| Metric | Research purpose |
|---|---|
| Precision | How many flagged country-years correspond to positive outcomes? |
| Recall | How many positive outcomes were identified? |
| F1-score | Summarises the balance between precision and recall at a chosen threshold |
| PR-AUC | Evaluates precision-recall ranking performance |
| ROC-AUC | Evaluates ranking discrimination |
| Brier score | Assesses probabilistic prediction error |
| Calibration | Checks agreement between predicted probabilities and observed frequencies |
| False-alarm rate | Examines unnecessary warnings |
| Missed-event analysis | Investigates outcomes the model failed to identify |

Metrics and decision thresholds will be selected using the research objective and validation data. Final test data must not be used to repeatedly tune the model.

## 8. Planned Visualisations

The following figures are planned research outputs, not existing results.

### Figure 1 — Historical conflict trends

A time-series chart showing annual conflict outcomes and changes over the study period.

### Figure 2 — Geographic distribution

A map showing documented historical outcomes or event patterns, with clear source attribution and data-coverage warnings.

### Figure 3 — Model comparison

A precision-recall curve or other appropriate comparison between the baseline and candidate models.

### Figure 4 — Probability calibration

A reliability diagram comparing predicted probabilities with observed outcome frequencies.

### Figure 5 — Error analysis

Charts examining false alarms, missed events and performance across relevant geographic and temporal groups.

### Figure 6 — Explainability

If an appropriate model is implemented, feature-contribution plots may help investigate why it produced particular estimates.

Feature importance and SHAP values describe model behaviour; they do not establish causal explanations for conflict.

## 9. Proposed Repository Structure

```text
AI-PeaceWatch/
├── README.md
├── CITATION.cff
├── LICENSE
├── requirements.txt
├── docs/
│   ├── research_protocol.md
│   ├── outcome_definition.md
│   ├── data_sources.md
│   ├── data_dictionary.md
│   ├── evaluation_plan.md
│   └── limitations.md
├── data/
│   ├── README.md
│   └── sample/
├── notebooks/
│   ├── 01_data_audit.ipynb
│   ├── 02_country_year_panel.ipynb
│   ├── 03_baseline_models.ipynb
│   └── 04_temporal_evaluation.ipynb
├── src/
│   ├── data_processing.py
│   ├── feature_engineering.py
│   ├── train.py
│   └── evaluate.py
├── tests/
├── figures/
└── reports/
```

This is the proposed structure. Files and directories should be added as implementation progresses.

Do not commit restricted datasets, credentials, personal information or large data files without checking permissions. Document how users can obtain data from its original source.

## 10. Limitations and Risks

### Data quality

Conflict records and socioeconomic indicators may be incomplete, delayed, revised or inconsistently measured.

### Rare outcomes

If positive outcomes are uncommon, apparently high accuracy may conceal poor detection performance.

### Temporal leakage

Using future information, revised measurements unavailable at forecast time or improperly constructed rolling features can inflate results.

### Geographic bias

Differences in reporting coverage and measurement quality can influence apparent patterns and model performance.

### Model uncertainty

Historical associations may not continue into the future. Political, social and economic systems can change in ways that historical models cannot anticipate.

### False alarms and missed events

A model may flag countries where the defined outcome does not occur or fail to flag countries where it does.

### Correlation versus causation

Predictive relationships do not establish that an indicator causes conflict.

### Ethical and political concerns

Incorrect predictions may stigmatise populations or be misused in consequential decisions.

AI PeaceWatch should therefore remain a research and decision-support project. Model outputs must not be treated as definitive judgements about countries, populations or political groups.

## 11. Responsible-AI Principles

The project will aim to:

- Document data provenance and variable definitions.
- Separate observed facts from model estimates.
- Report uncertainty and missing-data limitations.
- Evaluate errors across relevant regions and periods.
- Avoid claims of certainty unsupported by validation.
- Respect data licensing, privacy and security requirements.
- Maintain human oversight for consequential interpretation.
- Publish methodological limitations alongside findings.

## 12. Future Research Directions

Potential extensions include:

1. Comparing alternative definitions of conflict risk.
2. Evaluating multi-year forecasting horizons.
3. Exploring event-level and subnational geographic analysis.
4. Investigating additional socioeconomic and institutional indicators.
5. Testing alternative calibration and uncertainty-estimation methods.
6. Evaluating explainability methods with domain experts.
7. Developing an interactive research dashboard.
8. Exploring evidence-linked summaries and carefully governed alerts.
9. Evaluating whether the methods transfer to different historical periods and geographic settings.

Each extension will depend on data availability, methodological justification and the results of earlier experiments.

## 13. Expected Research Contribution

The project aims to produce a reproducible evaluation of whether historical conflict and socioeconomic data can support one-year-ahead conflict-outcome estimation.

Potential contributions include:

- A documented country-year data-processing workflow.
- A transparent comparison of simple baselines and machine-learning models.
- A temporal evaluation methodology.
- An analysis of prediction errors and uncertainty.
- Visualisations that make model performance understandable.
- A discussion of the methodological and ethical limits of early-warning systems.

These contributions remain proposed until supported by completed experiments and documented findings.

## 14. Getting Started

The initial development sequence is:

1. Review the selected dataset documentation.
2. Download and inspect the conflict data.
3. Select a small number of socioeconomic indicators.
4. Construct and validate the country-year panel.
5. Define the outcome and forecast horizon.
6. Establish a historical baseline.
7. Train and evaluate logistic regression.
8. Compare candidate models using temporal validation.
9. Document the results, errors and limitations.

Start with a reproducible notebook before building a full dashboard or production platform.

## Conclusion

AI PeaceWatch investigates how responsible data science can support the analysis of historical conflict patterns and potential early-warning indicators.

Its central principle is:

**Understand the data. Establish the baseline. Test the prediction. Communicate the uncertainty.**

The goal is not to claim that AI can predict every conflict, but to determine whether transparent, carefully evaluated analytical methods can provide useful evidence for researchers and human decision-makers.

---

**Project note:** This README describes a proposed research design. Datasets have not necessarily been integrated, models have not necessarily been trained, and predictive performance has not yet been established.
