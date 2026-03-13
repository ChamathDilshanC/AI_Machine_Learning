# 07 - Pipeline Deployment to Vertex AI

## Objective

Deploy an end-to-end sentiment inference pipeline to Vertex AI by uploading model artifacts, registering a model, creating/finding an endpoint, and deploying for online predictions.

## Files Included

| File                                                      | Purpose                                                           |
| --------------------------------------------------------- | ----------------------------------------------------------------- |
| `Deploy_Pipeline_to_Vertex_AI.ipynb`                      | Main deployment notebook                                          |
| `Deploy_Pipeline_to_Vertex_AI.example.ipynb`              | Example/template deployment notebook                              |
| `Linear_Classificaton - Logistic Regression Model .ipynb` | Source training workflow reused for deployment preparation        |
| `config.py`                                               | Configuration loader for project, region, bucket, model, endpoint |
| `model.joblib`                                            | Serialized trained model                                          |
| `vectorizer.joblib`                                       | Serialized text vectorizer                                        |
| `README.md`                                               | Module documentation                                              |

## What Is Implemented

1. Load deployment config from `.env`
2. Upload model artifacts to Google Cloud Storage
3. Register model in Vertex AI Model Registry (pre-built sklearn serving container)
4. Create a new endpoint or reuse an existing endpoint
5. Deploy model to endpoint with machine settings (`n1-standard-2` style)
6. Test inference using sample reviews

## Files and Artifact Explanations

| Type      | Meaning In This Module                                          |
| --------- | --------------------------------------------------------------- |
| `.ipynb`  | Deployment orchestration and validation notebook                |
| `.joblib` | Core deployable assets for model and preprocessing              |
| `.py`     | Centralized environment configuration for deployment parameters |

## Visualizations

| Visualization         | Status                | Description                               |
| --------------------- | --------------------- | ----------------------------------------- |
| Deployment Timeline   | Suggested Placeholder | Time per stage: upload, register, deploy  |
| Endpoint Test Summary | Suggested Placeholder | Prediction outputs from smoke-test inputs |
| Model Version Table   | Suggested Placeholder | Track registered model version history    |

## Vertex AI Deployment Guide

### 1. Prepare environment

```bash
gcloud auth login
gcloud config set project YOUR_PROJECT_ID
pip install -r ../requirements.txt
```

### 2. Configure this module

Create `.env` in this folder:

```env
GCP_PROJECT_ID=your-project-id
GCP_REGION=us-central1
GCS_BUCKET_NAME=your-bucket
MODEL_DISPLAY_NAME=sentiment-pipeline-v1
ENDPOINT_DISPLAY_NAME=sentiment-endpoint
GOOGLE_APPLICATION_CREDENTIALS=path/to/service-account.json
```

### 3. Run deployment notebook

```bash
jupyter notebook Deploy_Pipeline_to_Vertex_AI.ipynb
```

### 4. Validate

- Confirm model appears in Vertex AI Model Registry
- Confirm endpoint reaches deployed/healthy state
- Run sample predictions successfully

## Production Notes

- Keep model/vectorizer versions aligned and traceable
- Use unique display names per deployment iteration
- Monitor endpoint cost; undeploy/delete resources when idle
