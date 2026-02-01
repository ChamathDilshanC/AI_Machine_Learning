# Linear Classification - Sentiment Analysis

## Overview

This project demonstrates **Linear Classification** using **Logistic Regression** to perform sentiment analysis on women's clothing e-commerce reviews. The model classifies customer reviews as either positive or negative based on the review text.

## Dataset

- **Source**: Women's Clothing E-Commerce Reviews Dataset
- **File**: `womens_clothing_ecommerce_reviews.csv`
- **Features**:
  - `Review Text`: Customer review text (independent variable)
  - `sentiment`: Sentiment labels (1 = positive, -1 = negative)

## Project Workflow

### 1. **Data Loading**

- Load the dataset using pandas
- Display initial rows and dataset information to understand the structure

### 2. **Data Preparation**

- **Features (X)**: Review Text (raw text data)
- **Target (Y)**: Sentiment labels (1 or -1)
- **Train-Test Split**: 80% training, 20% testing with stratification to maintain class balance

### 3. **Text Vectorization**

- **Method**: Bag of Words using `CountVectorizer`
- **Stop Words Removal**: Common English words like "the", "is", "and" are removed
- Converts text reviews into numerical feature vectors for machine learning

### 4. **Model Training**

- **Algorithm**: Logistic Regression
- **Solver**: SAGA (suitable for large datasets)
- **Max Iterations**: 5000
- Learns the relationship between word frequencies and sentiment

### 5. **Model Evaluation**

- Make predictions on the test set
- Calculate accuracy score to measure performance
- Evaluate how well the model classifies unseen reviews

### 6. **Real-World Predictions**

- Test the trained model on new, unseen customer reviews
- Demonstrate the model's ability to classify real-world reviews

## Key Libraries Used

- **pandas**: Data manipulation and analysis
- **numpy**: Numerical computing
- **matplotlib & seaborn**: Data visualization
- **scikit-learn**: Machine learning tools
  - `train_test_split`: Split data into train/test sets
  - `CountVectorizer`: Convert text to numerical features
  - `LogisticRegression`: Classification model
  - `accuracy_score`: Performance evaluation

## How to Run

1. Ensure you have the required libraries installed:

   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn
   ```

2. Place the dataset file `womens_clothing_ecommerce_reviews.csv` in the parent directory

3. Open and run the Jupyter notebook:

   ```bash
   jupyter notebook Linear_Classificaton.ipynb
   ```

4. Execute all cells sequentially to:
   - Load and explore the data
   - Train the logistic regression model
   - Evaluate model performance
   - Make predictions on new reviews

## Expected Output

- Dataset information and statistics
- Training/testing data shapes
- Bag of Words representation and vocabulary size
- Model accuracy on test set
- Sentiment predictions for new customer reviews

## Learning Objectives

- Understand linear classification concepts
- Learn text preprocessing and vectorization (Bag of Words)
- Implement Logistic Regression for binary classification
- Evaluate model performance using accuracy metrics
- Apply trained models to predict sentiment on new data

## Notes

- The notebook includes detailed comments explaining each step
- Stratified splitting ensures balanced class distribution in train/test sets
- Stop words removal helps focus on meaningful words for sentiment analysis
- The model can be further improved with techniques like TF-IDF, hyperparameter tuning, or cross-validation
