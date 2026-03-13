# 02 - Multiple Linear Regression

## Objective

Extend regression from one feature to multiple features by modeling `Sales` from `TV`, `Radio`, and `Newspaper` advertising spends.

## Files Included

| File                               | Purpose                                                                            |
| ---------------------------------- | ---------------------------------------------------------------------------------- |
| `Multiple_Linear_Regression.ipynb` | Multivariate regression notebook with scaling, SGD training, and metric evaluation |
| `README.md`                        | Module documentation                                                               |

## What Is Implemented

1. Load `advertising.csv`
2. Define multi-feature matrix (`TV`, `Radio`, `Newspaper`)
3. Apply train/test split
4. Normalize features with `StandardScaler`
5. Train `SGDRegressor`
6. Evaluate with `MAE`, `MSE`, `RMSE`
7. Predict for new ad-budget combinations

## Visualizations

| Visualization             | Status                | Description                                                 |
| ------------------------- | --------------------- | ----------------------------------------------------------- |
| Feature Relationship Plot | Implied in workflow   | Supports understanding multi-feature impact before training |
| Predicted vs Actual       | Suggested Placeholder | Scatter plot of predicted sales against true sales          |
| Residual Distribution     | Suggested Placeholder | Histogram or KDE of residual errors for model diagnostics   |

## Files and Artifacts Notes

- `.ipynb`: Contains data prep, scaling, model training, and evaluation sequence
- `.py`: Not required in this module (notebook-centered learning stage)
- `.joblib`: Not generated in this module by default, but can be added for model persistence

## Skills Demonstrated

- Multivariate regression
- Feature scaling for SGD convergence
- Error-metric-based model validation
- Applied predictive analytics from structured tabular data

## Run

```bash
jupyter notebook Multiple_Linear_Regression.ipynb
```
