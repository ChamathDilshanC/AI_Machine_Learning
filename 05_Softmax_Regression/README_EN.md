# Softmax Regression on MNIST Dataset

This project demonstrates how to use **Softmax Regression** (a generalization of Logistic Regression for multi-class classification) to classify handwritten digits from the famous **MNIST dataset**.

## Project Overview

The notebook covers the complete pipeline of a machine learning project:

1.  **Data Loading**: Fetching the MNIST dataset using `sklearn.datasets.fetch_openml`.
2.  **Data Exploration**: Visualizing sample images and checking data dimensions to understand the input.
3.  **Preprocessing**: Normalizing pixel values to the 0-1 range (dividing by 255.0) for better model convergence.
4.  **Model Training**: Training a Softmax Regression model using `sklearn.linear_model.LogisticRegression` with the 'lbfgs' solver.
5.  **Evaluation**: Measuring accuracy on a test set (unseen data) and visualizing performance with a Confusion Matrix to see where the model makes mistakes.
6.  **Prediction**: Testing the trained model on randomly selected samples to demonstrate real-world usage.

### Prerequisites

To run this notebook, you need the following libraries:

- `python` (3.x)
- `numpy` (For numerical operations)
- `matplotlib` (For data visualization)
- `scikit-learn` (For machine learning model and dataset)

### How to Run

1.  Install dependencies: `pip install numpy matplotlib scikit-learn`
2.  Open the notebook `Softmax_Regression.ipynb`.
3.  Run all cells sequentially.
