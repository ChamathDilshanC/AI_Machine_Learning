# ✅ Pre-Commit Checklist

Before pushing to GitHub, run these verification steps to ensure no sensitive data is exposed.

## 1. Create Test .env Files

Create sample .env files in each directory to test:

```powershell
# In PowerShell
cd C:\Users\chamm\Desktop\AI_Machine_Learning

# Create test .env files
cd 06_Get_Online_Inference
Copy-Item .env.example .env
cd ..

cd 07_Pipeline_Deployment
Copy-Item .env.example .env
cd ..

cd 08_Hit_Pipeline_Deployment
Copy-Item .env.example .env
cd ..
```

## 2. Check Git Status

```powershell
# This should NOT show any .env or config.py files
git status
```

### ❌ Files that should NOT appear:

- `06_Get_Online_Inference/.env`
- `06_Get_Online_Inference/config.py`
- `07_Pipeline_Deployment/.env`
- `07_Pipeline_Deployment/config.py`
- `08_Hit_Pipeline_Deployment/.env`
- `08_Hit_Pipeline_Deployment/config.py`
- `*.joblib` files
- `*.csv` files

### ✅ Files that SHOULD appear:

- `06_Get_Online_Inference/.env.example`
- `07_Pipeline_Deployment/.env.example`
- `08_Hit_Pipeline_Deployment/.env.example`
- `*.example.ipynb` files
- `.gitignore`
- `requirements.txt`
- Documentation files

## 3. Explicit Check with git check-ignore

```powershell
# Check if .env files are properly ignored
git check-ignore 06_Get_Online_Inference/.env
git check-ignore 07_Pipeline_Deployment/.env
git check-ignore 08_Hit_Pipeline_Deployment/.env

# Each command should return the filename (meaning it's ignored)
```

## 4. Test Add Command

```powershell
# Try to add a specific .env file - should be ignored
git add 06_Get_Online_Inference/.env

# Check status - should not show the .env file being added
git status
```

## 5. Visual Inspection

Open each directory and verify:

### 06_Get_Online_Inference/

- [ ] `.env.example` exists (safe for git)
- [ ] `.env` will be created by user (gitignored)
- [ ] `config.py` exists (gitignored)
- [ ] `*.example.ipynb` exists (safe for git)

### 07_Pipeline_Deployment/

- [ ] `.env.example` exists (safe for git)
- [ ] `.env` will be created by user (gitignored)
- [ ] `config.py` exists (gitignored)
- [ ] `*.example.ipynb` exists (safe for git)

### 08_Hit_Pipeline_Deployment/

- [ ] `.env.example` exists (safe for git)
- [ ] `.env` will be created by user (gitignored)
- [ ] `config.py` exists (gitignored)
- [ ] `*.example.ipynb` exists (safe for git)

## 6. .gitignore Verification

Check that `.gitignore` contains these patterns:

```bash
# View .gitignore
cat .gitignore | Select-String -Pattern ".env|config.py|*.joblib|*.csv"
```

Should show:

- `.env`
- `config.py`
- `*.joblib`
- `*.csv`

## 7. Final Safe Push Test

```powershell
# Stage all files
git add .

# Show what will be committed
git status

# Show detailed diff (should not contain sensitive data)
git diff --cached

# If everything looks good, commit
git commit -m "Initial commit: ML project with directory-specific configs"
```

## 8. Post-Push Verification

After pushing to GitHub:

1. Go to your GitHub repository
2. Check that `.env` files are NOT visible
3. Check that `config.py` files are NOT visible
4. Verify `.env.example` files ARE visible
5. Verify example notebooks ARE visible

## 🚨 If You Accidentally Commit Sensitive Data

### Option 1: If you haven't pushed yet

```powershell
# Undo the commit but keep files
git reset --soft HEAD~1

# Remove from staging
git reset HEAD <file-with-sensitive-data>
```

### Option 2: If you already pushed

```powershell
# DANGER: This rewrites history
# Remove file from git history
git filter-branch --force --index-filter   "git rm --cached --ignore-unmatch <file-path>"   --prune-empty --tag-name-filter cat -- --all

# Force push (WARNING: Coordinate with team)
git push --force --all
```

### Option 3: For sensitive data in commits

- Consider regenerating any exposed API keys or credentials
- Update your GCP project settings if project IDs were exposed
- Enable 2FA and additional security measures

## ✅ All Clear Checklist

Before final push, confirm:

- [ ] `git status` shows no `.env` files
- [ ] `git status` shows no `config.py` files (except examples)
- [ ] `git status` shows no `.joblib` or `.csv` files
- [ ] Only `*.example` files are being committed
- [ ] Documentation files are included
- [ ] `.gitignore` is present and configured
- [ ] Test `git check-ignore` on sensitive files returns the filename

## 🎉 Ready to Push!

If all checks pass, you're safe to push:

```powershell
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/AI_Machine_Learning.git
git push -u origin main
```

Your sensitive data is protected! 🔒
