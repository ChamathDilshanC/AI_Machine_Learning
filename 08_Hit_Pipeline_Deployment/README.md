# 08 - Hit Pipeline Deployment Endpoint

## Objective

Validate deployed Vertex AI pipeline behavior by sending prediction requests and verifying inference responses for single and batch inputs.

## Files Included

| File                                   | Purpose                                           |
| -------------------------------------- | ------------------------------------------------- |
| `08_Pipeline_Deployment.example.ipynb` | Endpoint hit/testing example notebook             |
| `config.py`                            | Loads endpoint runtime settings from local `.env` |
| `README.md`                            | Module documentation                              |

## What Is Implemented

1. Load endpoint config from `.env`
2. Initialize Vertex AI client
3. Resolve target endpoint by display name
4. Build test instances
5. Send prediction requests (`endpoint.predict(...)`)
6. Display and verify response payloads

## Files and Artifact Explanations

| Type      | Meaning In This Module                                                  |
| --------- | ----------------------------------------------------------------------- |
| `.ipynb`  | Endpoint invocation/testing notebook                                    |
| `.joblib` | Optional at this stage; primarily needed in training/deployment modules |
| `.py`     | Configuration utility for endpoint test execution                       |

## Visualizations

| Visualization             | Status                | Description                                      |
| ------------------------- | --------------------- | ------------------------------------------------ |
| Batch Prediction Table    | Suggested Placeholder | Input review vs returned prediction              |
| Error Case Review         | Suggested Placeholder | Misclassified examples for quick diagnosis       |
| Endpoint Response Latency | Suggested Placeholder | Time per request to estimate runtime performance |

## Endpoint Test Instructions (Vertex AI)

### 1. Configure this module

Create `.env` in this folder:

```env
GCP_PROJECT_ID=your-project-id
GCP_REGION=us-central1
ENDPOINT_DISPLAY_NAME=sentiment-endpoint
GOOGLE_APPLICATION_CREDENTIALS=path/to/service-account.json
```

### 2. Run test notebook

```bash
jupyter notebook 08_Pipeline_Deployment.example.ipynb
```

### 3. Validate output

- Endpoint is discovered by display name
- Prediction array length matches input instance count
- Output classes are logically consistent for sample text

## Troubleshooting

- `Endpoint not found`: verify region and endpoint display name
- `Permission denied`: verify service account and IAM roles
- `Schema mismatch`: ensure input format matches deployed model expectations
