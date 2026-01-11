# 📊 Multiple Linear Regression - Advertising & Sales Analysis

A comprehensive implementation of Multiple Linear Regression to predict product sales based on TV, Radio, and Newspaper advertising spending. This project demonstrates advanced regression concepts using Stochastic Gradient Descent (SGD) with scikit-learn and Python.

## 🎯 Project Overview

This project analyzes the combined effect of multiple advertising channels (TV, Radio, Newspaper) on product sales, building a predictive model that considers all three features simultaneously. The analysis uses SGD Regressor with feature scaling to optimize model performance and follows a complete machine learning workflow from data preparation to model evaluation and prediction.

## 📁 Project Structure

```
Multiple_Linear_Regression/
├── Multiple_Linear_Regression.ipynb    # Main Jupyter notebook with complete analysis
└── README.md                            # Project documentation
```

## 🔧 Technologies Used

- **Python 3.x**
- **pandas** - Data manipulation and analysis
- **numpy** - Numerical computing
- **matplotlib** - Data visualization
- **seaborn** - Statistical data visualization
- **scikit-learn** - Machine learning library
  - SGDRegressor - Stochastic Gradient Descent regression
  - StandardScaler - Feature normalization
  - train_test_split - Data splitting
  - metrics - Model evaluation

## 📊 Dataset

The project uses the **Advertising Dataset** (`advertising.csv`) which contains:

- **TV**: TV advertising budget (in thousands of dollars)
- **Radio**: Radio advertising budget (in thousands of dollars)
- **Newspaper**: Newspaper advertising budget (in thousands of dollars)
- **Sales**: Product sales (in thousands of units)

**Note**: This project uses Multiple Linear Regression with all three advertising channels as predictor variables.

## 🚀 Getting Started

### Prerequisites

Install the required packages:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

### Running the Notebook

1. Navigate to the project directory:

```bash
cd Multiple_Linear_Regression
```

2. Launch Jupyter Notebook:

```bash
jupyter notebook Multiple_Linear_Regression.ipynb
```

3. Run all cells sequentially to reproduce the analysis

## 📈 Analysis Workflow

### 1. **Import Required Libraries**

- Load all necessary Python libraries for data analysis and machine learning
- Import SGDRegressor and StandardScaler for model training

### 2. **Data Loading**

- Load the advertising dataset
- Display first few rows to understand data structure

### 3. **Feature Selection**

- Select TV, Radio, and Newspaper as independent variables (X)
- Select Sales as the dependent variable (Y)
- Handle multiple features for multivariate analysis

### 4. **Data Splitting**

- Split data into training (80%) and testing (20%) sets
- Ensure reproducibility with random_state=42
- Maintain data integrity across train-test split

### 5. **Feature Scaling**

- Create StandardScaler to normalize features
- Fit scaler on training data to avoid data leakage
- Transform both training and testing sets
- **Why scaling?** SGD requires normalized features for optimal convergence

### 6. **Model Training**

- Create SGDRegressor with optimized parameters:
  - `max_iter=1000`: Number of training epochs
  - `tol=1e-4`: Convergence tolerance
  - `random_state=42`: Reproducibility
- Fit the model on scaled training data
- Learn the relationship: **Sales = Intercept + (coef₁ × TV) + (coef₂ × Radio) + (coef₃ × Newspaper)**

### 7. **Model Parameters**

- Extract and display intercept and coefficients
- Interpret the linear equation
- Understand the contribution of each advertising channel

### 8. **Model Evaluation**

- Make predictions on the test set
- Calculate performance metrics:
  - **MSE (Mean Squared Error)**: Average squared prediction error
  - **RMSE (Root Mean Squared Error)**: Standard deviation of prediction errors
  - **MAE (Mean Absolute Error)**: Average absolute prediction error

### 9. **New Predictions**

- Predict sales for new advertising budget combinations
- Apply the same scaling transformation to new data
- Generate actionable predictions for business decisions

## 📊 Key Results

The model learns a multiple linear relationship of the form:

```
Sales = Intercept + (coef[0] × TV) + (coef[1] × Radio) + (coef[2] × Newspaper)
```

- **Intercept**: Baseline sales when all advertising spending is $0
- **Coefficients**: Individual impact of each advertising channel on sales

### Model Performance

The model is evaluated using three key metrics:

- **Mean Absolute Error (MAE)**: Average prediction error in thousands of units
- **Mean Squared Error (MSE)**: Penalizes larger errors more heavily
- **Root Mean Squared Error (RMSE)**: Prediction error in original units (thousands)

## 💡 Key Insights

- Multiple features provide more accurate predictions than single-feature models
- Different advertising channels have varying impacts on sales
- Feature scaling is crucial for SGD convergence and model performance
- The model can predict sales for any combination of advertising budgets

## 🎓 Learning Objectives

This project demonstrates:

- ✅ Multiple Linear Regression implementation
- ✅ Stochastic Gradient Descent optimization
- ✅ Feature scaling with StandardScaler
- ✅ Train-test split methodology
- ✅ Model evaluation with multiple metrics
- ✅ Making predictions on new data
- ✅ Understanding multivariate relationships

## 🔄 Differences from Simple Linear Regression

| Feature                | Simple Linear Regression | Multiple Linear Regression |
| ---------------------- | ------------------------ | -------------------------- |
| **Number of Features** | 1 (TV only)              | 3 (TV, Radio, Newspaper)   |
| **Model Complexity**   | y = mx + b               | y = b + m₁x₁ + m₂x₂ + m₃x₃ |
| **Algorithm**          | LinearRegression         | SGDRegressor               |
| **Feature Scaling**    | Not required             | Required for SGD           |
| **Insights**           | Single factor impact     | Combined factor effects    |

## 🔮 Future Enhancements

- [ ] Add R² (coefficient of determination) metric
- [ ] Perform feature importance analysis
- [ ] Implement polynomial features for non-linear relationships
- [ ] Add residual analysis and diagnostic plots
- [ ] Compare with other regression algorithms (Ridge, Lasso, ElasticNet)
- [ ] Implement cross-validation for robust evaluation
- [ ] Create interactive visualizations for predictions
- [ ] Add hyperparameter tuning for SGD

## 📝 Notes

- The dataset is assumed to be in the parent directory (`../advertising.csv`)
- All code cells include detailed comments explaining each step
- Feature scaling is essential for SGD convergence
- The notebook is designed for educational purposes

## 🤝 Contributing

Feel free to fork this project and submit pull requests for improvements or additional features.

## 📄 License

This project is open source and available for educational purposes.

---

**Created**: January 2026
**Last Updated**: January 11, 2026
