# 🩺 Silent Risk — Predicting Chronic Disease Before It Strikes

> **A health analytics project built for a fictional national health insurer (MutuelSanté), using the CDC BRFSS 2024 survey to predict diabetes risk and chronic disease multi-morbidity before clinical diagnosis.**

---

## Business Context

Health insurers operate reactively — claims arrive, costs are absorbed, interventions come too late. Chronic diseases develop silently for years before surfacing as expensive medical events.

This project builds a predictive risk engine that scores members on diabetes risk using behavioral and demographic data alone — no clinical measurements required. The model enables proactive prevention, geographic prioritization of resources, and early identification of high-risk undetected members.

**Estimated business impact at threshold 0.20:** $19.3M net benefit on a 90k-member test set, based on US average cost benchmarks ($12,000 annual diabetic member cost, $300 prevention program cost, 40% early detection savings rate).

---

## The 3 Business Questions

**Q1.** Which profiles present the highest risk of diabetes or multi-morbidity, and how can they be identified before diagnosis?

**Q2.** In which states and socioeconomic segments is under-utilization of healthcare most critical?

**Q3.** Which modifiable behaviors are the most actionable levers to reduce risk in the short term?

---

## Dataset

| Property | Detail |
|---|---|
| Source | CDC — Centers for Disease Control and Prevention |
| Survey | Behavioral Risk Factor Surveillance System (BRFSS) |
| Year | 2024 |
| Format | SAS XPT |
| Respondents | 457,670 US adults |
| Variables | 301 |

Dataset available at: https://www.cdc.gov/brfss/annual_data/annual_2024.html

> The raw data file is not versioned in this repo due to size (1GB). Download the XPT file from the CDC link above and place it in `data/raw/`.

---

## Project Structure
```
silent-risk-chronic-disease/
├── data/
│   ├── raw/          # BRFSS 2024 XPT file (not versioned)
│   └── processed/    # Cleaned datasets (not versioned)
├── notebooks/
│   └── silent_risk_brfss_2024.ipynb
├── reports/
│   └── silent_risk_presentation.pptx
└── README.md
```

---

## Notebook Structure

| Section | Content |
|---|---|
| 0 | Introduction & dataset architecture |
| 1 | Business framing — stakeholders, error costs, 3 business questions |
| 2 | EDA — demographics, income, behaviors, healthcare access, geography |
| 3 | Feature engineering — BMI, behavioral risk score, multi-morbidity score, under-care index |
| 4 | Modeling — logistic regression baseline, LightGBM, Optuna, calibration, threshold selection, secondary model |
| 5 | Interpretability — SHAP global, alternative model, risk tiers, undetected profile, individual SHAP, threshold simulation |
| 6 | Business recommendations — 4 action levers, financial simulation, next steps |
| 7 | SQL analysis — SQLite in-memory, business queries on 453k rows |
| 8 | Interactive Plotly dashboard |

---

## Key Results

### Model Performance

| Model | AUC-ROC | Recall (Diabetic) | Precision |
|---|---|---|---|
| Logistic Regression (baseline) | 0.8051 | 0.75 | 0.31 |
| LightGBM (main model) | 0.8216 | 0.69 | 0.35 |
| LightGBM (no protected attributes) | 0.8031 | — | — |

**Selected threshold:** 0.20 — captures 68.6% of diabetics while flagging 28.5% of the portfolio.

### Risk Tier Segmentation

| Tier | Population | Diabetes Rate | Action |
|---|---|---|---|
| 1 — Low | 52.7% | 3.4% | Standard annual checkup |
| 2 — Moderate | 18.8% | 14.6% | Targeted prevention communication |
| 3 — High | 20.3% | 28.8% | Active prevention program |
| 4 — Critical | 8.2% | 50.4% | Immediate proactive screening |

### Top SHAP Features

1. `_AGEG5YR` — Age (dominant predictor)
2. `GENHLTH` — Self-reported general health
3. `CHECKUP1` — Time since last checkup (reverse causality)
4. `BMI` — Body mass index
5. `ALCDAY4` — Alcohol consumption (reverse causality)
6. `CHCKDNY2` — Kidney disease diagnosis
7. `EXERANY2` — Physical activity
8. `state_diabetes_rate` — Geographic context

### Geographic Findings

| Highest Risk | Rate | Lowest Risk | Rate |
|---|---|---|---|
| West Virginia | 21.7% | Colorado | 9.8% |
| Kentucky | 20.3% | Vermont | 10.5% |
| South Carolina | 19.6% | Massachusetts | 10.6% |

12-point gap between highest and lowest states. The Diabetes Belt (Appalachian + Southeastern states) is clearly visible.

---

## Derived Features

| Feature | Description | Signal |
|---|---|---|
| `BMI` | Computed from height & weight | Obese: 22.7% vs Normal: 7.6% |
| `BEHAVIORAL_RISK_SCORE` | Smoking + sedentary + alcohol + obesity (0-4) | Score 0: 10.7% → Score 4: 25.7% |
| `MULTIMORBIDITY_SCORE` | Count of 10 chronic conditions | Score 0: 7.5% → Score 10: 76.2% |
| `UNDERCARE_INDEX` | No doctor + cost barrier + no checkup (0-3) | Captures likely-undetected risk |

---

## Stack

| Category | Tools |
|---|---|
| Data | Python, Pandas, NumPy |
| Visualization | Seaborn, Matplotlib, Plotly |
| Modeling | Scikit-learn, LightGBM, Optuna |
| Interpretability | SHAP |
| SQL | SQLite (in-memory) |
| Environment | Conda (Python 3.11) |

---

## Deliverables

- `notebooks/silent_risk_brfss_2024.ipynb` — Full analysis notebook
- `reports/silent_risk_presentation.pptx` — 16-slide business presentation
- Interactive Plotly dashboard embedded in notebook (Section 8)

---

## Author

**Arvind Bajolah** — Data Analyst