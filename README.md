# ml_regression_sgolla

A compact regression analysis project that models and predicts medical insurance charges using the `insurance.csv` dataset. The work is implemented in a single Jupyter Notebook (`regression_sgolla.ipynb`) and demonstrates data exploration, preprocessing with `ColumnTransformer`/`Pipeline`, and model comparisons across Linear Regression, Ridge Regression, and Polynomial Regression.

**Author:** Saratchandra Golla
**Date:** November 24, 2025

## Project Overview
- **Goal:** Predict continuous insurance charges and compare model performance using R², MAE, and RMSE.
- **Models included:** Baseline Linear Regression, Ridge Regression (alpha=10.0), Polynomial Regression (degree=3).
- **Key steps:** EDA, preprocessing (scaling & one-hot encoding), pipeline training, diagnostic plots, and model comparison (including a visualization cell that plots R², MAE and RMSE for each model).

## Repository structure
- `regression_sgolla.ipynb` : Primary notebook containing analysis, models, and visualizations.
- `data/insurance.csv`    : Dataset (Medical Cost Personal Datasets).
- `requirements.txt`      : Python dependencies used for the notebook.

## Setup
1. (Optional) Create and activate a virtual environment.

Powershell example:
```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

2. Install dependencies:
```powershell
python -m pip install --upgrade pip
pip install -r requirements.txt
```

3. Open the notebook in Jupyter or VS Code and run cells top-to-bottom to reproduce results:
```powershell
jupyter notebook regression_sgolla.ipynb
```

## Reproducing Results
- Run all cells in `regression_sgolla.ipynb` in order. The notebook trains three models, prints evaluation metrics, and includes an added visualization cell that shows side-by-side bar plots for R², MAE, and RMSE (sorted by R²).
- If you run notebook cells out of order, rerun the model training cells (`4.2`, `5.1`, `5.2`) before running the model comparison/visualization cell.

## Notes & Next Steps
- The notebook flags heteroscedasticity in residuals; the Polynomial Regression improved performance by modeling nonlinear interactions.
- If you have more time: perform hyperparameter tuning (GridSearchCV, RandomizedSearchCV or Bayesian optimization), try ensemble/tree models (Random Forest, XGBoost), experiment with target transforms, and add model-interpretability (SHAP) and saved model artifacts for deployment.

