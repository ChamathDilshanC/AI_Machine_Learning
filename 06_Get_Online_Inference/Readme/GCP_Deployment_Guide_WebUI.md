# 🌐 GCP Deployment Guide - Web UI / Console Method

මේ Guide එකෙන් අපි බලමු කොහොමද **Command Line / Codes** ලියන්නේ නැතුව, Google Cloud Console WEBSITE එක හරහා පමණක් machine learning model එකක් deploy කරන්නේ කියලා.

---

## 📋 අන්තර්ගතය

1.  [Prerequisites (මූලික අවශ්‍යතා)](#1-prerequisites-මූලික-අවශ්‍යතා)
2.  [Model Training (Local)](#2-model-training-local)
3.  [Method: Google Cloud Console (Web UI) භාවිතා කර Deploy කිරීම](#3-method-google-cloud-console-web-ui-භාවිතා-කර-deploy-කිරීම)
4.  [Test කිරීම](#4-test-කිරීම)

---

## 1. Prerequisites (මූලික අවශ්‍යතා)

මුලින්ම මේ දේවල් හදාගෙන ඉන්න ඕනේ.

1.  **Google Cloud Account එකක්**: [Console එක](https://console.cloud.google.com/) හරහා log වෙන්න.
2.  **Project එකක් Create කරන්න**: Project ID එක මතක තියාගන්න.
3.  **Billing Enable කරන්න**: Project එකට Billing add කරන්න.
4.  **API Enable කරන්න**: **Vertex AI API** සහ **Cloud Storage API** console එකෙන් enable කරන්න.

---

## 2. Model Training (Local)

ඔයා තවම model එකක් train කරලා නැත්නම්, ඔයාගේ computer එකේදී `model.joblib` එකක් හදාගන්න. මේකට Python ඕනේ වෙනවා.

```python
# train.py
from sklearn.datasets import load_iris
from sklearn.ensemble import RandomForestClassifier
import joblib

# Load Data & Train
iris = load_iris()
model = RandomForestClassifier(n_estimators=100)
model.fit(iris.data, iris.target)

# Save
joblib.dump(model, 'model.joblib')
print("✅ Model saved as 'model.joblib'")
```

දැන් ඔයා ළඟ `model.joblib` file එක තියෙනවා. අපි දැන් මේක Web UI එකෙන් deploy කරමු.

---

## 3. Method: Google Cloud Console (Web UI) භාවිතා කර Deploy කිරීම

### Step 1: Model එක Bucket එකට Upload කිරීම

1.  **Google Cloud Console** එකේ [Google Cloud Storage](https://console.cloud.google.com/storage/browser) වෙත යන්න.
2.  **CREATE** click කරලා අලුත් bucket එකක් හදන්න (නමක් දෙන්න, region එක `us-central1` දෙන්න).
3.  Bucket එක ඇතුලට ගිහින් **UPLOAD FILES** click කරලා ඔයාගේ `model.joblib` file එක upload කරන්න.

### Step 2: Vertex AI Model Registry එකට Import කිරීම

1.  Console menu එකෙන් **Vertex AI** -> **Model Registry** වෙත යන්න.
2.  **IMPORT** click කරන්න.
3.  **Import as new model** තෝරන්න.
4.  **Name**: නමක් දෙන්න (උදා: `iris-model-ui`).
5.  **Region**: `us-central1` තෝරන්න. **CONTINUE**.
6.  **Model Settings**:
    - **Framework**: `scikit-learn`
    - **Framework version**: `1.0` (හෝ අදාළ version එක)
    - **Pre-built container**: මෙය auto-select වෙයි.
    - **Model artifact location**: `BROWSE` click කරලා bucket එකේ `model.joblib` තියෙන **folder එක** (file එක නෙවෙයි) select කරන්න.
7.  **IMPORT** click කරන්න.

### Step 3: Endpoint එකක් හදලා Deploy කිරීම

1.  Model එක import වුනාට පස්සේ Registry list එකේ ඒක click කරන්න.
2.  **DEPLOY TO ENDPOINT** click කරන්න.
3.  **Define your endpoint**: "Create new endpoint" තෝරලා නමක් දෙන්න. **CONTINUE**.
4.  **Model settings**:
    - **Machine type**: `n1-standard-2` (හෝ `e2-standard-2`) තෝරන්න.
    - **DEPLOY** click කරන්න.

විනාඩි 10-15කින් Endpoint එක active වෙයි (Green tick එකක් වැටෙයි).

---

## 4. Test කිරීම

Deploy වුනාට පස්සේ Endpoint එක ඇතුලට ගිහින් **"Test your model"** tab එකක් තියෙනවා ද බලන්න. එහෙම නැත්නම්, පහත Python code එකෙන් test කරන්න පුළුවන්.

```python
# test.py
from google.cloud import aiplatform

PROJECT_ID = "YOUR_PROJECT_ID"
ENDPOINT_NAME = "iris-endpoint-ui" # ඔයා දුන්න නම

aiplatform.init(project=PROJECT_ID, location="us-central1")

endpoints = aiplatform.Endpoint.list(filter=f'display_name="{ENDPOINT_NAME}"')
if endpoints:
    endpoint = endpoints[0]
    print("Prediction:", endpoint.predict(instances=[[5.1, 3.5, 1.4, 0.2]]).predictions)
```

---

### ⚠️ Clean Up

වැඩේ ඉවර වුනාම Console එකෙන් Endpoint එක සහ ID එක delete කරන්න, නැත්නම් බිල එන්න පුළුවන්.
