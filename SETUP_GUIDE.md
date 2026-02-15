# 🔐 GitHub & Configuration Setup Guide

This guide explains how to safely share your ML projects on GitHub while keeping sensitive information private.

## 📁 What's in This Repository?

### ✅ Safe to Commit (Public Files)

- `*/.env.example` - Templates for environment variables (in each directory)
- `config.example.py` - Template for configuration
- `*.example.ipynb` - Example notebooks with placeholders
- `requirements.txt` - Python dependencies
- `.gitignore` - Files to exclude from git
- `README.md` - Project documentation

### ❌ Never Commit (Private Files - in `.gitignore`)

- `.env` - Your actual credentials (in each directory)
- `config.py` - Your actual project IDs (in each directory)
- `*.joblib` - Trained model files (too large)
- `*.csv` - Data files
- `__pycache__/` - Python cache
- `.ipynb_checkpoints/` - Jupyter checkpoints

## 📂 Directory-Specific Configuration

Each directory that needs GCP credentials has its own `.env` file:

- **06_Get_Online_Inference/** - For testing deployed models
- **07_Pipeline_Deployment/** - For deploying pipelines to Vertex AI
- **08_Hit_Pipeline_Deployment/** - For testing deployed pipelines

This allows each notebook to have its own configuration independently.

## 🚀 Quick Start for GitHub

### For Repository Owner (You):

1. **Initial Git Setup**

   ```bash
   cd AI_Machine_Learning
   git init
   git add .
   git commit -m "Initial commit with example files"
   git branch -M main
   git remote add origin <your-github-repo-url>
   git push -u origin main
   ```

2. **Your Private Configuration**
   - Keep your actual notebooks (without `.example` extension)
   - Keep your `config.py` with real values
   - Keep your `.env` with real credentials
   - These are already in `.gitignore` and won't be committed

### For Others Cloning Your Repository:

1. **Clone the Repository**

   ```bash
   git clone <your-github-repo-url>
   cd AI_Machine_Learning
   ```

2. **Install Dependencies**

   ```bash
   pip install -r requirements.txt
   ```

3. **Set Up Configuration for Each Directory**

   Each directory (06, 07, 08) has its own `.env.example` file. Copy and configure them:

   ```bash
   # For 06_Get_Online_Inference
   cd 06_Get_Online_Inference
   cp .env.example .env
   notepad .env  # Windows (or nano .env for Linux/Mac)
   # Fill in: GCP_PROJECT_ID, GCP_REGION, ENDPOINT_DISPLAY_NAME
   cd ..

   # For 07_Pipeline_Deployment
   cd 07_Pipeline_Deployment
   cp .env.example .env
   notepad .env
   # Fill in: GCP_PROJECT_ID, GCP_REGION, GCS_BUCKET_NAME, etc.
   cd ..

   # For 08_Hit_Pipeline_Deployment
   cd 08_Hit_Pipeline_Deployment
   cp .env.example .env
   notepad .env
   # Fill in: GCP_PROJECT_ID, GCP_REGION, ENDPOINT_DISPLAY_NAME
   cd ..
   ```

4. **Authenticate with Google Cloud**
   ```bash
   gcloud auth application-default login
   ```

## 🔧 Configuration Methods

### Method 1: Directory-Specific .env Files (Recommended)

**Advantages:**

- ✅ Each notebook has its own configuration
- ✅ Industry standard approach
- ✅ Easy to maintain different settings per notebook
- ✅ No risk of configuration conflicts

**Setup:**

1. Navigate to each directory (06, 07, 08)
2. Copy `.env.example` to `.env` in that directory
3. Fill in your values in each `.env`
4. The `config.py` in each directory automatically loads from its local `.env`

**Example .env for 06_Get_Online_Inference:**

```env
GCP_PROJECT_ID=my-actual-project-123
GCP_REGION=us-central1
ENDPOINT_DISPLAY_NAME=my-endpoint
```

**Example .env for 07_Pipeline_Deployment:**

```env
GCP_PROJECT_ID=my-actual-project-123
GCP_REGION=us-central1
GCS_BUCKET_NAME=my-ml-bucket
MODEL_DISPLAY_NAME=sentiment-model
ENDPOINT_DISPLAY_NAME=sentiment-endpoint
LOCAL_MODEL_PATH=model.joblib
```

### Method 2: Direct Configuration in Notebooks

**Advantages:**

- ✅ Simpler for beginners
- ✅ No additional files needed
- ✅ Clear and visible

**Setup:**

1. Copy example notebooks (remove `.example` from filename)
2. Uncomment the direct configuration section
3. Fill in your values directly in the notebook

**Example:**

```python
PROJECT_ID = "my-actual-project-123"
REGION = "us-central1"
ENDPOINT_DISPLAY_NAME = "my-endpoint"
```

## 📋 Configuration Checklist

Before running notebooks, make sure you have:

- [ ] Installed Python dependencies (`pip install -r requirements.txt`)
- [ ] Created `.env` file in the directory you're working with (copied from `.env.example`)
- [ ] Filled in your GCP credentials in the `.env` file
- [ ] Authenticated with GCP (`gcloud auth application-default login`)
- [ ] Enabled required APIs (Vertex AI, Cloud Storage)
- [ ] Created GCS bucket (if using deployment notebooks - 07_Pipeline_Deployment)

## 🔄 Workflow Example

### 1. Your Local Setup (Not on GitHub)

```
AI_Machine_Learning/
├── 06_Get_Online_Inference/
│   ├── .env                      # ❌ Your credentials (gitignored)
│   ├── config.py                 # ❌ Generated config (gitignored)
│   └── 06_Get_Online_Inference.ipynb  # ❌ Your notebook (gitignored)
├── 07_Pipeline_Deployment/
│   ├── .env                      # ❌ Your credentials (gitignored)
│   ├── config.py                 # ❌ Generated config (gitignored)
│   ├── Deploy_Pipeline_to_Vertex_AI.ipynb  # ❌ (gitignored)
│   └── model.joblib              # ❌ Model file (gitignored)
├── 08_Hit_Pipeline_Deployment/
│   ├── .env                      # ❌ Your credentials (gitignored)
│   └── config.py                 # ❌ Generated config (gitignored)
└── womens_clothing_ecommerce_reviews.csv  # ❌ Data (gitignored)
```

### 2. What Goes to GitHub (Public)

```
AI_Machine_Learning/
├── .gitignore                    # ✅ Exclude rules
├── requirements.txt              # ✅ Dependencies
├── README.md                     # ✅ Documentation
├── SETUP_GUIDE.md               # ✅ This guide
├── 06_Get_Online_Inference/
│   ├── .env.example              # ✅ Template
│   └── 06_Get_Online_Inference.example.ipynb  # ✅ Template
├── 07_Pipeline_Deployment/
│   ├── .env.example              # ✅ Template
│   └── Deploy_Pipeline_to_Vertex_AI.example.ipynb  # ✅ Template
└── 08_Hit_Pipeline_Deployment/
    ├── .env.example              # ✅ Template
    └── 08_Pipeline_Deployment.example.ipynb  # ✅ Template
```

### 3. Others Clone and Configure

```bash
git clone <repo>
cd AI_Machine_Learning

# Set up each directory
cd 06_Get_Online_Inference
cp .env.example .env
# Edit .env with their credentials
cd ..

cd 07_Pipeline_Deployment
cp .env.example .env
# Edit .env
cd ..

cd 08_Hit_Pipeline_Deployment
cp .env.example .env
# Edit .env
cd ..

# Run notebooks - each uses its own config
```

## 🛡️ Security Best Practices

1. **Never commit sensitive data**
   - Project IDs
   - API keys
     -Credentials
   - Personal data

2. **Review before committing**

   ```bash
   git status  # Check what will be committed
   git diff    # Review changes
   ```

3. **Verify .gitignore is working**

   ```bash
   git status  # Should NOT show .env, config.py, *.joblib, etc.
   ```

4. **If you accidentally commit secrets**

   ```bash
   # Remove from git history (use with caution!)
   git filter-branch --force --index-filter \
     "git rm --cached --ignore-unmatch path/to/secret/file" \
     --prune-empty --tag-name-filter cat -- --all

   # Then force push (WARNING: rewrites history)
   git push --force --all
   ```

## 📞 Common Issues

### Issue: Notebooks can't find config.py

**Solution:** Make sure `config.py` is in the project root directory

### Issue: "No module named 'dotenv'"

**Solution:** Install python-dotenv

```bash
pip install python-dotenv
```

### Issue: "Permission denied" when accessing GCP

**Solution:** Authenticate with gcloud

```bash
gcloud auth application-default login
```

### Issue: Example notebooks have placeholder values

**Solution:** Copy to real notebook and configure

```bash
cp notebook.example.ipynb notebook.ipynb
# Then edit notebook.ipynb with your values
```

## 📚 Additional Resources

- [Google Cloud Authentication](https://cloud.google.com/docs/authentication)
- [Git Ignore Documentation](https://git-scm.com/docs/gitignore)
- [Python dotenv](https://github.com/theskumar/python-dotenv)
- [Vertex AI Documentation](https://cloud.google.com/vertex-ai/docs)

## 🎯 Summary

✅ **Safe to share:** Example files, templates, documentation
❌ **Never share:** Your credentials, project IDs, trained models
🔒 **Protected by:** `.gitignore` file
🔧 **Configuration:** Use `.env` or `config.py` (both gitignored)

---

**Ready to push to GitHub?** Follow the Quick Start section above! 🚀
