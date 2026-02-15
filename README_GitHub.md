# AI & Machine Learning Projects

This repository contains various machine learning projects and notebooks demonstrating different ML techniques.

## 📋 Setup Instructions

### 1. Clone the Repository

```bash
git clone <your-repo-url>
cd AI_Machine_Learning
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure Google Cloud (For Vertex AI Projects)

Each directory that uses Google Cloud has its own `.env` configuration file.

#### Set up configuration for each notebook:

```bash
# For getting online inference (06)
cd 06_Get_Online_Inference
cp .env.example .env
# Edit .env and fill in: GCP_PROJECT_ID, GCP_REGION, ENDPOINT_DISPLAY_NAME
cd ..

# For pipeline deployment (07)
cd 07_Pipeline_Deployment
cp .env.example .env
# Edit .env and fill in: GCP_PROJECT_ID, GCP_REGION, GCS_BUCKET_NAME, etc.
cd ..

# For testing pipeline deployment (08)
cd 08_Hit_Pipeline_Deployment
cp .env.example .env
# Edit .env and fill in: GCP_PROJECT_ID, GCP_REGION, ENDPOINT_DISPLAY_NAME
cd ..
```

**Why separate .env files?**

- Each notebook can have its own configuration
- No conflicts between different notebooks
- Easier to manage different environments
- Industry standard approach

### 4. Authenticate with Google Cloud

```bash
gcloud auth application-default login
```

## 📁 Project Structure

```
AI_Machine_Learning/
├── 01_Single_Linear_Regression/
├── 02_Multiple_Linear_Regression/
├── 03_Linear_Classificaton (Logistic Regression Model)/
├── 04_Unsupervised_Learnining_Clustering/
├── 05_Softmax_Regression/
├── 06_Get_Online_Inference/
│   ├── .env.example                 # Configuration template
│   ├── config.py                    # Auto-generated (gitignored)
│   └── *.example.ipynb              # Example notebooks
├── 07_Pipeline_Deployment/
│   ├── .env.example                 # Configuration template
│   ├── config.py                    # Auto-generated (gitignored)
│   └── *.example.ipynb              # Example notebooks
├── 08_Hit_Pipeline_Deployment/
│   ├── .env.example                 # Configuration template
│   ├── config.py                    # Auto-generated (gitignored)
│   └── *.example.ipynb              # Example notebooks
├── requirements.txt                 # Python dependencies
├── .gitignore                       # Git ignore rules
└── README.md                        # This file
```

## 🚀 Usage

### Running Notebooks

Each folder contains Jupyter notebooks with detailed instructions. Start with:

```bash
jupyter notebook
```

### Deploying to Google Cloud Vertex AI

See notebooks in folders:

- `07_Pipeline_Deployment/` - Train and deploy model
- `08_Hit_Pipeline_Deployment/` - Test deployed model

## 📝 Important Notes

⚠️ **Never commit sensitive information:**

- `.env` files in any directory (contain your credentials)
- `config.py` files in any directory (auto-generated from .env)
- `.joblib` files (ML model files - too large)
- `.csv` data files (if they contain sensitive data)

✅ **Safe to commit:**

- `.env.example` files (templates only)
- `*.example.ipynb` files (notebook templates with placeholders)
- Documentation files (README, SETUP_GUIDE, etc.)
- `requirements.txt`

## 🔒 Security

- All sensitive files are listed in `.gitignore`
- Each directory has its own `.env` file for isolation
- Use `.env.example` as templates
- Never share your actual project IDs or credentials
- Use `.env.example` as a template
- Never share your actual project IDs or credentials

## 📚 Projects Included

1. **Single Linear Regression** - Basic linear regression
2. **Multiple Linear Regression** - Multi-variable regression
3. **Logistic Regression** - Binary classification
4. **Clustering** - Unsupervised learning
5. **Softmax Regression** - Multi-class classification
6. **Online Inference** - Get predictions from deployed models
7. **Pipeline Deployment** - Deploy ML pipelines to Google Cloud
8. **Hit Pipeline** - Test and use deployed pipelines

## 🛠 Requirements

See `requirements.txt` for full list. Main dependencies:

- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn
- google-cloud-aiplatform
- google-cloud-storage
- python-dotenv
- joblib

## 📧 Contact

For questions or issues, please open an issue on GitHub.
