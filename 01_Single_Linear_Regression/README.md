# 01 - Single Linear Regression

## Objective

Build a foundational regression model that predicts `Sales` from `TV` advertising spend using a single-feature linear regression workflow.

## Files Included

| File                      | Purpose                                                                                    |
| ------------------------- | ------------------------------------------------------------------------------------------ |
| `Linear_Regression.ipynb` | End-to-end notebook: EDA, train/test split, model fit, equation extraction, and prediction |
| `README.md`               | Module documentation                                                                       |

## What Is Implemented

1. Load `advertising.csv`
2. Explore feature-target relationships with pairplots
3. Select a single predictor (`TV`) and target (`Sales`)
4. Train `LinearRegression` from scikit-learn
5. Extract intercept and coefficient for model interpretability
6. Predict on test data and sample new inputs

## Visualizations

| Visualization             | Status                | Description                                                         |
| ------------------------- | --------------------- | ------------------------------------------------------------------- |
| Pairplot                  | Implemented           | Relationship overview for `TV`, `Radio`, `Newspaper`, `Sales`       |
| Scatter + Regression Line | Implemented           | Best-fit line over real observations                                |
| Residual Plot             | Suggested Placeholder | Add `y_test - y_pred` vs predicted values to diagnose bias/patterns |

## Skills Demonstrated

- Regression fundamentals
- Baseline model building
- Train/test validation split
- Linear equation interpretation

## Run

```bash
jupyter notebook Linear_Regression.ipynb
```
