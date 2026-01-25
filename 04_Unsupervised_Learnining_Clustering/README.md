# Unsupervised Learning - Document Clustering

This project demonstrates how to use Unsupervised Learning techniques to cluster text documents. Specifically, we use **K-Means Clustering** to categorize Wikipedia articles into three distinct topics: **Astrophysics**, **Biology**, and **Computer Science**.

## File Description: `04_Unsupervised_Learnining_Clustering.ipynb`

This Jupyter Notebook is the core file of the project. It contains the complete end-to-end pipeline for clustering text documents.

### Notebook Structure

The notebook is organized into the following logical sections:

1.  **Imports & Setup**: Loads necessary libraries (`wikipedia-api`, `nltk`, `sklearn`) and handles SSL context for secure data fetching.
2.  **API Testing**: Verifies connectivity to Wikipedia by fetching a sample page ("Sigiriya").
3.  **Data Loading**: Defines a list of 9 articles across 3 domains (Astrophysics, Biology, CS) and downloads their content.
4.  **Preprocessing**: Applies text cleaning techniques (lowercase, regex removal) and Lemmatization to prepare the text for analysis.
5.  **Vectorization**: Uses `TfidfVectorizer` to transform the raw text into a matrix of numerical features (keeping the top 1000 words).
6.  **Model Training**: Initializes and trains a `KMeans` clustering model with $k=3$ and `n_init=20` for stable results.
7.  **Evaluation**:
    - Calculates **WCSS** (Inertia) to check cluster compactness.
    - Computes **Silhouette Score** to measure how well-separated the clusters are.
8.  **Prediction**: A final demonstration cell that takes new, unseen sentences (e.g., about Hubble or DNA) and predicts which cluster they belong to.

## Key Concepts

- **Unsupervised Learning**: The model learns patterns (clusters) from data without labeled answers.
- **TF-IDF**: Weighs words by importance (common words like "the" get low scores; specific words like "galaxy" get high scores).
- **K-Means**: Iteratively moves 3 centroids to minimize the distance between data points and their assigned center.

## Author

CHamath Dilshan
