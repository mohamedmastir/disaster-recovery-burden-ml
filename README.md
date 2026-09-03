# Explainable Machine Learning for Anticipating County-Level Disaster Recovery Burden

This repository provides the conceptual workflow, data sources, and computational environment for the paper:

> *"Explainable machine learning for anticipating county-level disaster recovery burden in the built environment"*
> Manuscript ID: IJDRBE-06-2026-0116
> Journal: International Journal of Disaster Resilience in the Built Environment

## Overview

This study develops an explainable machine-learning framework to anticipate county-level high recovery burden from natural disasters one year ahead using only public administrative and social-vulnerability data. The framework compares class-weighted logistic regression, random forest, and XGBoost models under a strictly forward-looking temporal validation design.

## Data Sources

The analytical pipeline relies exclusively on publicly available data:

| Source | Description | Access |
|--------|-------------|--------|
| FEMA Disaster Declarations Summaries | Declared events and assistance-programme categories | [OpenFEMA](https://www.fema.gov/about-openfema) |
| CDC/ATSDR Social Vulnerability Index (SVI) | County-level social and demographic vulnerability | [CDC SVI](https://www.atsdr.cdc.gov/placeandhealth/svi/) |

## Conceptual Pipeline

The preprocessing and modeling workflow follows these steps:

1. **Data Integration**: Merging FEMA and SVI datasets using standard county FIPS codes and aligning temporal dimensions (2014–2022).
2. **Feature Engineering**: Calculating one-year lagged features and three-year rolling means/maxima for event duration, prior program burden, and SVI themes.
3. **Target Construction**: Defining the positive class as county-years with ≥ 2 disaster declarations carrying Public Assistance and/or Hazard Mitigation flags.
4. **Model Training & Validation**: Training Class-Weighted Logistic Regression, Random Forest, and XGBoost. Hyperparameters tuned on the 2020 validation set.
5. **Evaluation**: Out-of-sample evaluation on the 2021–2022 hold-out set using AUROC, PR AUC, F1-score, Precision, Recall, and Brier score.
6. **Explainability**: Extracting standardized coefficients for the logistic model and SHAP values for the XGBoost model.

## Key Design Decisions

- **Temporal split**: 2014–2019 (train), 2020 (validation), 2021–2022 (test) to prevent data leakage.
- **Class weighting** selected over synthetic oversampling (e.g., SMOTE) to preserve the real-world distribution of demographic and administrative variables.
- **Decision thresholds** optimized on the validation year to maximize F1-score, applied unchanged to the test set.

## Reproducibility

The exact analytical pipeline can be reconstructed using the variables and procedures reported in the manuscript. The required computational environment and dependencies are listed in `requirements.txt`.

## Citation

If you use this conceptual framework or workflow, please cite the original paper :

## License

This conceptual workflow is provided for academic and research purposes.
