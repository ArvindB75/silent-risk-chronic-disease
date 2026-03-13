# Silent Risk — Predicting Chronic Disease Before It Strikes

## Business Context
A national health insurer wants to identify high-risk members before they develop costly chronic conditions. This project leverages the CDC BRFSS 2024 survey (~400k respondents) to predict diabetes risk and multi-morbidity, and to map prevention priorities geographically.

## Business Questions
1. Which profiles present the highest risk of diabetes or multi-morbidity, and how can they be identified before diagnosis?
2. In which states and socioeconomic segments is under-utilization of healthcare most critical?
3. Which modifiable behaviors are the most actionable levers to reduce risk in the short term?

## Project Structure
```
silent-risk-chronic-disease/
├── data/
│   ├── raw/          # Original BRFSS 2024 XPT file (not versioned)
│   └── processed/    # Cleaned datasets (not versioned)
├── notebooks/        # Jupyter notebooks
├── src/              # Python modules
├── reports/
│   └── figures/      # Exported visualizations
└── README.md
```

## Stack
Python, Pandas, NumPy, Seaborn, Matplotlib, Plotly, Scikit-learn, LightGBM, SHAP, SQLite

## Dataset
CDC Behavioral Risk Factor Surveillance System (BRFSS) 2024
Source: https://www.cdc.gov/brfss/annual_data/annual_2024.html
