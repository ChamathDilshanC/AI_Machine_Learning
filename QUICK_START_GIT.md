# 🚀 Quick Start - Git Commands

## For You (Repository Owner)

### Initial Setup

```bash
# Navigate to your project
cd C:\Users\chamm\Desktop\AI_Machine_Learning

# Initialize git repository
git init

# Add all files (safe files only, .gitignore protects sensitive data)
git add .

# Check what will be committed (verify no sensitive files)
git status

# Commit the files
git commit -m "Initial commit: ML project with example templates"

# Create main branch
git branch -M main

# Add your GitHub repository as remote
# Replace <your-username> with your GitHub username
git remote add origin https://github.com/<your-username>/AI_Machine_Learning.git

# Push to GitHub
git push -u origin main
```

### Updating Later

```bash
# Check what changed
git status

# Add new files or changes
git add .

# Commit changes
git commit -m "Your commit message here"

# Push to GitHub
git push
```

## For Others (Cloning Your Repo)

```bash
# Clone the repository
git clone https://github.com/<your-username>/AI_Machine_Learning.git
cd AI_Machine_Learning

# Install dependencies
pip install -r requirements.txt

# Set up configuration for each directory
cd 06_Get_Online_Inference
cp .env.example .env
# Edit .env with your GCP project details
cd ..

cd 07_Pipeline_Deployment
cp .env.example .env
# Edit .env with your GCP details including bucket name
cd ..

cd 08_Hit_Pipeline_Deployment
cp .env.example .env
# Edit .env with your GCP details
cd ..

# Authenticate with Google Cloud
gcloud auth application-default login

# Start Jupyter
jupyter notebook
```

## Verification Checklist

Before pushing to GitHub, verify:

```bash
# Check git status - sensitive files should NOT appear
git status

# These files should be UNTRACKED (gitignored):
# - 06_Get_Online_Inference/.env
# - 06_Get_Online_Inference/config.py
# - 07_Pipeline_Deployment/.env
# - 07_Pipeline_Deployment/config.py
# - 07_Pipeline_Deployment/model.joblib
# - 08_Hit_Pipeline_Deployment/.env
# - 08_Hit_Pipeline_Deployment/config.py
# - *.csv files
# - Any non-.example notebooks

# These files SHOULD be tracked:
# - 06_Get_Online_Inference/.env.example
# - 07_Pipeline_Deployment/.env.example
# - 08_Hit_Pipeline_Deployment/.env.example
# - *.example.ipynb files
# - .gitignore
# - requirements.txt
# - README files
```

# - \*.example.ipynb

# - .gitignore

# - requirements.txt

# - README.md, SETUP_GUIDE.md

````

## Common Git Commands

```bash
# See what changed
git diff

# See commit history
git log --oneline

# Undo uncommitted changes
git checkout -- filename

# Undo last commit (keep changes)
git reset --soft HEAD~1

# Create a new branch
git checkout -b feature-name

# Switch branches
git checkout main

# Pull latest changes
git pull origin main
````

## 🔒 Security Check

**Before your first push, verify these files are ignored:**

```bash
# Check if sensitive files are properly ignored
cd 06_Get_Online_Inference
git check-ignore .env config.py
cd ..

cd 07_Pipeline_Deployment
git check-ignore .env config.py model.joblib
cd ..

cd 08_Hit_Pipeline_Deployment
git check-ignore .env config.py
cd ..

# Check data files
git check-ignore *.csv

# All these should show as "Ignored"
```

## 📝 Example .gitignore (Already Created)

Your `.gitignore` file already protects:

- `.env` (your credentials - in all directories)
- `config.py` (your project IDs - in all directories)
- `*.joblib` (model files)
- `*.csv` (data files)
- `__pycache__/` (Python cache)
- `.ipynb_checkpoints/` (Jupyter checkpoints)

## ✅ You're Ready!

1. Run the "Initial Setup" commands above
2. Verify with the "Security Check"
3. Push to GitHub
4. Share the repository!

Your sensitive data is protected! 🔒
