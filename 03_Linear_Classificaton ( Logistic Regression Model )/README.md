# 03 - Linear Classification (Logistic Regression Model)

## Objective

Train a binary NLP classifier that predicts review sentiment (`1` positive, `-1` negative) from raw customer review text.

## Files Included

| File                                                      | Purpose                                                                      |
| --------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `Linear_Classificaton - Logistic Regression Model .ipynb` | Main notebook: text preprocessing, vectorization, model training, evaluation |
| `README.md`                                               | Module documentation                                                         |

## What Is Implemented

1. Load `womens_clothing_ecommerce_reviews.csv`
2. Select `Review Text` as feature and `sentiment` as label
3. Use stratified train/test split for class-balance consistency
4. Convert text to Bag-of-Words vectors with `CountVectorizer(stop_words="english")`
5. Train `LogisticRegression` (`solver='saga'`, `max_iter=5000`)
6. Evaluate with accuracy and run sample real-world predictions

## Files and Artifact Explanations

| Type      | Meaning In This Module                                                                  |
| --------- | --------------------------------------------------------------------------------------- |
| `.ipynb`  | Research notebook containing full NLP classification pipeline                           |
| `.joblib` | Not mandatory here, but this model is later serialized and reused in deployment modules |
| `.py`     | Not used in this folder; deployment modules use `config.py` for runtime settings        |

## Visualizations

| Visualization       | Status                | Description                                            |
| ------------------- | --------------------- | ------------------------------------------------------ |
| Label Distribution  | Suggested Placeholder | Bar chart for class balance (`positive` vs `negative`) |
| Top Token Frequency | Suggested Placeholder | Most frequent words after stop-word removal            |
| Confusion Matrix    | Suggested Placeholder | Classification error profile beyond plain accuracy     |

## Notes for Recruiters

- Demonstrates practical NLP classification without deep learning dependencies
- Uses proper train/test strategy with stratification
- Produces reusable model behavior later integrated into Vertex AI workflows

## Run

```bash
jupyter notebook "Linear_Classificaton - Logistic Regression Model .ipynb"
```
