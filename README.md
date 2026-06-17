[README.md](https://github.com/user-attachments/files/29035581/README.md)
# PSX Financial Distress Early Warning System

A four-stage machine learning framework for predicting financial distress
among non-financial firms listed on the Pakistan Stock Exchange (PSX),
covering FY2011–FY2024.

---

## Overview

This repository contains the full implementation of the study comparing
within-pipeline SMOTE against hierarchical severity decomposition across
six tree-based and ensemble classifiers, with a twelve-module Explainable
AI (XAI) audit.

**Four distress stages:**
- Stage 0 — Healthy
- Stage 1 — Profit Reduction
- Stage 2 — Mild Liquidity Distress
- Stage 3 — Severe Liquidity Distress

**Best model:** SMOTE + Decision Tree | Macro Recall = 0.777 | Stage 3 Recall = 0.897

---

## Repository Contents

| File | Description |
|------|-------------|
| `PSX_Distress_EarlyWarning_CLEAN.ipynb` | Full pipeline: data cleaning, modelling, XAI audit |

---

## Data

Data is sourced from the **Financial Statements Analysis of the
Non-Financial Companies (FSANFC)**, published by the State Bank of
Pakistan (2023, 2024, 2025). The raw data is not included in this
repository as it is publicly available directly from the SBP:
https://www.sbp.org.pk/reports/annual/FSANFC/Years.htm

---

## Requirements

```
python >= 3.11
pandas
numpy
scikit-learn >= 1.0
imbalanced-learn
lightgbm >= 4.0
xgboost >= 2.0
shap
lime
matplotlib
seaborn
google-colab (for Drive mount)
```

Install all dependencies by running **§1** of the notebook.

---

## How to Run

1. Open `PSX_Distress_EarlyWarning_CLEAN.ipynb` in Google Colab
2. Mount your Google Drive (§2) — outputs and checkpoints save there
3. Place the raw FSANFC Excel file at the path defined in §3
4. Run all cells sequentially from §1 to §16

All stochastic components are seeded with `random_state=42` for
bit-for-bit reproducibility.

---

## Pipeline Summary

| Section | Description |
|---------|-------------|
| §1–§2 | Dependencies, imports, Drive mount |
| §3–§4 | Data loading and T+1 target engineering |
| §5–§6 | Cleaning pipeline and temporal split |
| §7–§8 | Imputation, scaling, feature selection |
| §9–§10 | Model configurations and evaluation framework |
| §11 | Experiment A — SMOTE (flat four-class) |
| §12 | Experiment B — Hierarchical Decomposition |
| §13–§14 | Master comparison and visualisations |
| §15-XAI | Twelve-module XAI audit (SHAP, LIME, PDPs, surrogate trees, bootstrap stability) |
| §16 | Save all artefacts |

---

## Results Summary

| Model | Macro Recall | Stage 1 Recall | Stage 2 Recall | Stage 3 Recall |
|-------|-------------|----------------|----------------|----------------|
| SMOTE + Decision Tree ★ | 0.777 | 0.944 | 0.584 | 0.897 |
| SMOTE + LightGBM | 0.770 | 0.907 | 0.591 | 0.897 |
| SMOTE + Random Forest | 0.767 | 0.879 | 0.620 | 0.885 |
| Hierarchical S1 | 0.749 | 0.879 | 0.606 | 0.859 |

★ Selected model for XAI audit.

---

## License

This code is released for academic reproducibility purposes.
For any other use, please contact the authors.
