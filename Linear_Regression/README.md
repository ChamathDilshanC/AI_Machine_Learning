# 📊 Simple Linear Regression - TV Advertising & Sales Analysis

A comprehensive implementation of Simple Linear Regression to predict product sales based on TV advertising spending. This project demonstrates the fundamental concepts of linear regression using scikit-learn and Python.

## 🎯 Project Overview

This project analyzes the relationship between TV advertising expenditure and product sales, building a predictive model to estimate sales based on advertising budget. The analysis follows a complete machine learning workflow from data exploration to model evaluation and prediction.

## 📁 Project Structure

```
Linear_Regression/
├── Linear_Regression.ipynb    # Main Jupyter notebook with complete analysis
├── pairplot.png                # Visualization of variable relationships
├── regression_line.png         # Linear regression plot
└── README.md                   # Project documentation
```

## 🔧 Technologies Used

- **Python 3.x**
- **pandas** - Data manipulation and analysis
- **numpy** - Numerical computing
- **matplotlib** - Data visualization
- **seaborn** - Statistical data visualization
- **scikit-learn** - Machine learning library

## 📊 Dataset

The project uses the **Advertising Dataset** (`advertising.csv`) which contains:

- **TV**: TV advertising budget (in thousands of dollars)
- **Radio**: Radio advertising budget (in thousands of dollars)
- **Newspaper**: Newspaper advertising budget (in thousands of dollars)
- **Sales**: Product sales (in thousands of units)

**Note**: This project focuses on Simple Linear Regression using only TV advertising as the predictor variable.

## 🚀 Getting Started

### Prerequisites

Install the required packages:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

### Running the Notebook

1. Navigate to the project directory:

```bash
cd Linear_Regression
```

2. Launch Jupyter Notebook:

```bash
jupyter notebook Linear_Regression.ipynb
```

3. Run all cells sequentially to reproduce the analysis

## 📈 Analysis Workflow

### 1. **Data Loading & Exploration**

- Load the advertising dataset
- Display dataset structure and statistics
- Check for missing values and data types

### 2. **Exploratory Data Analysis (EDA)**

- Visualize relationships between variables using pairplots
- Identify correlations between features and target variable

![Pairplot of Dataset](pairplot.png)
_Figure 1: Pairplot showing relationships between all variables in the dataset_

### 3. **Feature Selection**

- Select TV advertising as the independent variable (X)
- Select Sales as the dependent variable (y)

### 4. **Data Splitting**

- Split data into training (80%) and testing (20%) sets
- Ensure reproducibility with random_state=42

### 5. **Model Training**

- Create a Linear Regression model
- Fit the model on training data
- Learn the linear relationship: **Sales = Intercept + (Coefficient × TV)**

### 6. **Model Parameters**

- Extract and display intercept and coefficient
- Interpret the linear equation

### 7. **Visualization**

- Plot actual vs. predicted sales
- Display the regression line on test data

![Regression Line](regression_line.png)
_Figure 2: Linear regression line fitted to TV advertising vs. sales data_

### 8. **Predictions**

- Make predictions on new TV advertising budgets
- Evaluate model performance

## 📊 Key Results

The model learns a linear relationship of the form:

```
Sales = Intercept + (Coefficient × TV)
```

- **Intercept**: Baseline sales when TV spending is $0
- **Coefficient**: Sales increase per $1,000 spent on TV advertising

### Visual Results

The analysis produces two key visualizations:

1. **Pairplot**: Shows the distribution and relationships between all variables (TV, Radio, Newspaper, Sales)
2. **Regression Line Plot**: Displays the linear relationship between TV advertising spending and sales, with actual data points (blue) and the fitted regression line (red)

## 💡 Key Insights

- Strong positive correlation between TV advertising and sales
- For every additional $1,000 spent on TV ads, sales increase by approximately [coefficient] thousand units
- The model provides a simple yet effective baseline for sales prediction

## 🎓 Learning Objectives

This project demonstrates:

- ✅ Simple Linear Regression implementation
- ✅ Train-test split methodology
- ✅ Model training and parameter extraction
- ✅ Data visualization techniques
- ✅ Making predictions with trained models
- ✅ Understanding the linear relationship between variables

## 🔮 Future Enhancements

- [ ] Implement Multiple Linear Regression using all features (TV, Radio, Newspaper)
- [ ] Add model evaluation metrics (R², MSE, RMSE, MAE)
- [ ] Perform residual analysis
- [ ] Add cross-validation
- [ ] Compare with polynomial regression
- [ ] Create interactive visualizations

## 📝 Notes

- The dataset is assumed to be in the parent directory (`../advertising.csv`)
- All code cells include detailed comments explaining each step
- The notebook is designed for educational purposes

## 🤝 Contributing

Feel free to fork this project and submit pull requests for improvements or additional features.

## 📄 License

This project is open source and available for educational purposes.

---

**Created**: December 2025
**Last Updated**: December 21, 2025
