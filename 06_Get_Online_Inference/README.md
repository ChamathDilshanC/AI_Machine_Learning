# 06 - Get Online Inference

## Objective

Call a deployed Vertex AI endpoint for real-time sentiment predictions using a previously trained model and vectorizer.

## Files Included

| File                                    | Purpose                                       |
| --------------------------------------- | --------------------------------------------- |
| `06_Get_Online_Inference.ipynb`         | Main notebook for endpoint prediction flow    |
| `06_Get_Online_Inference.example.ipynb` | Example/template notebook                     |
| `config.py`                             | Loads runtime settings from local `.env`      |
| `model.joblib`                          | Saved sentiment model artifact (local copy)   |
| `vectorizer.joblib`                     | Saved text vectorizer artifact                |
| `request.json`                          | Example request payload for inference testing |
| `README.md`                             | Module documentation                          |

## What Is Implemented

1. Load configuration from `.env` via `config.py`
2. Initialize Vertex AI SDK (`google.cloud.aiplatform`)
3. Resolve endpoint by display name
4. Prepare and vectorize text input
5. Send prediction requests to endpoint
6. Print prediction outputs for online inference validation

## Files and Artifact Explanations

| Type      | Meaning In This Module                                                |
| --------- | --------------------------------------------------------------------- |
| `.ipynb`  | Online inference execution flow and quick experiments                 |
| `.joblib` | Serialized model/vectorizer used as inference artifacts               |
| `.py`     | Configuration utility for environment variables and endpoint settings |

## Visualizations

| Visualization                          | Status                | Description                                               |
| -------------------------------------- | --------------------- | --------------------------------------------------------- |
| Prediction Distribution                | Suggested Placeholder | Count of predicted sentiment classes from batch inference |
| Confidence Trend (if scores available) | Suggested Placeholder | Confidence values over multiple test reviews              |

## Configuration

Create a local `.env` in this folder with values such as:

```env
GCP_PROJECT_ID=your-project-id
GCP_REGION=us-central1
ENDPOINT_DISPLAY_NAME=your-endpoint-name
GOOGLE_APPLICATION_CREDENTIALS=path/to/service-account.json
```

## Run

```bash
jupyter notebook 06_Get_Online_Inference.ipynb
```

## Deployment Context

This module assumes the model is already deployed to Vertex AI endpoint (typically completed in module 07).
