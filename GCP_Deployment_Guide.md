# 🚀 Google Cloud (Vertex AI) Deployment Guide - Step by Step

මේ Guide එකෙන් අපි බලමු කොහොමද **Docker පාවිච්චි කරන්නේ නැතුව**, ඔයාගේ Machine Learning model එකක් Google Cloud Platform (GCP) එකේ Vertex AI හරහා deploy කරගන්නේ කියලා. අපි පාවිච්චි කරන්නේ **Pre-built Containers** ක්‍රමයයි. මේක තමයි ලේසිම සහ වේගවත්ම ක්‍රමය.

---

## 📋 අන්තර්ගතය (Table of Contents)

1.  [Prerequisites (මූලික අවශ්‍යතා)](#1-prerequisites-මූලික-අවශ්‍යතා)
2.  [Environment Setup (පරිගණකය සකසා ගැනීම)](#2-environment-setup-පරිගණකය-සකසා-ගැනීම)
3.  [Project Structure එක හදාගැනීම](#3-project-structure-එක-හදාගැනීම)
4.  [Model Train කිරීම](#4-model-train-කිරීම)
5.  [Google Cloud Storage (GCS) Bucket එකක් සෑදීම](#5-google-cloud-storage-gcs-bucket-එකක්-සෑදීම)
6.  [Vertex AI වෙත Model එක Deploy කිරීම (Python Code)](#6-vertex-ai-වෙත-model-එක-deploy-කිරීම)
7.  [Method 2: Google Cloud Console (Web UI) භාවිතා කර Deploy කිරීම](#7-method-2-google-cloud-console-web-ui-භාවිතා-කර-deploy-කිරීම)
8.  [Test කිරීම](#8-test-කිරීම)

---

## 1. Prerequisites (මූලික අවශ්‍යතා)

මුලින්ම මේ දේවල් හදාගෙන ඉන්න ඕනේ.

1.  **Google Cloud Account එකක්**:
    - [Google Cloud Console](https://console.cloud.google.com/) එකට ගිහින් Gmail එකෙන් log වෙන්න.
    - අලුත් Account එකක් නම් $300 free credit හම්බවෙනවා.

2.  **New Project එකක් Create කරන්න**:
    - Console එකේ උඩ වම් පැත්තේ තියෙන Project dropdown එක click කරලා "New Project" දෙන්න.
    - නමක් දෙන්න (උදා: `my-ml-project`).
    - **Project ID** එක මතක තියාගන්න (මේක unique වෙන්න ඕනේ).

3.  **Billing Enable කරන්න**:
    - Project එක select කරලා, වම් පැත්තේ menu එකෙන් "Billing" වලට ගිහින් card details දීලා billing enable කරන්න (Free trial එක use කරන්න පුළුවන්).

4.  **API Enable කරන්න**:
    - Search bar එකේ **"Vertex AI API"** කියලා search කරලා ඒක _Enable_ කරන්න.
    - ඊළඟට **"Cloud Storage API"** කියලා search කරලා ඒකත් _Enable_ කරන්න.

---

## 2. Environment Setup (පරිගණකය සකසා ගැනීම)

ඔයාගේ local computer එකේ මේවා install කරගන්න.

1.  **Google Cloud SDK (gcloud CLI) Install කරන්න**:
    - [Download gcloud CLI](https://cloud.google.com/sdk/docs/install) ලින්ක් එකෙන් ගිහින් install කරගන්න.
    - Install වුනාට පස්සේ terminal එකේ (CMD/Powershell) මේ command එක ගහලා login වෙන්න:
      ```bash
      gcloud auth login
      ```
    - ඊළඟට ඔයාගේ project එක set කරගන්න:
      ```bash
      gcloud config set project YOUR_PROJECT_ID
      ```
      _( `YOUR_PROJECT_ID` වෙනුවට ඔයා කලින් හදාගත්ත Project ID එක දාන්න)_

2.  **Python Libraries Install කරන්න**:
    ```bash
    pip install google-cloud-aiplatform google-cloud-storage scikit-learn pandas joblib
    ```

---

## 3. Project Structure එක හදාගැනීම

ඔයාගේ වැඩේට folder එකක් හදාගෙන මේ විදියට files ටික තියාගන්න.

```text
my-ml-deploy/
├── train.py          # Model එක train කරන code එක
├── deploy.py         # Model එක GCP එකට යවන code එක
├── test.py           # Deploy වුනාට පස්සේ check කරන code එක
└── requirements.txt  # (Optional)
```

---

## 4. Model Train කිරීම

මුලින්ම අපි Scikit-learn model එකක් හදලා ඒක `model.joblib` විදියට save කරගන්න ඕනේ. Google pre-built containers support කරන්නේ `model.joblib`, `model.pkl`, හෝ `model.bst` වගේ formats වලට.

**`train.py`** ෆයිල් එක හදන්න:

```python
# train.py
from sklearn.datasets import load_iris
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split
import joblib

# 1. Data load කරගන්න
print("Loading data...")
iris = load_iris()
X, y = iris.data, iris.target
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# 2. Model එක train කරන්න
print("Training model...")
model = RandomForestClassifier(n_estimators=100)
model.fit(X_train, y_train)

# 3. Model එක Local save කරගන්න
# නම අනිවාර්යයෙන්ම 'model.joblib' විය යුතුයි.
joblib.dump(model, 'model.joblib')

print(f"Model accuracy: {model.score(X_test, y_test):.2f}")
print("✅ Model saved as 'model.joblib'")
```

මේක run කරන්න:

```bash
python train.py
```

දැන් ඔයාට `model.joblib` ෆයිල් එක හැදිලා ඇති.

---

## 5. Google Cloud Storage (GCS) Bucket එකක් සෑදීම

අපේ model file එක Vertex AI එකට දෙන්න කලින්, ඒක Cloud Storage Bucket එකක දාන්න ඕනේ.

1.  **Bucket එකක් හදන්න** (නම unique වෙන්න ඕනේ, උදා: `my-model-bucket-2024`):

    ```bash
    # us-central1 region එකේ bucket එකක් හදනවා
    gsutil mb -l us-central1 gs://YOUR-UNIQUE-BUCKET-NAME
    ```

2.  **Model එක Upload කරන්න**:
    ```bash
    gsutil cp model.joblib gs://YOUR-UNIQUE-BUCKET-NAME/model.joblib
    ```

---

## 6. Vertex AI වෙත Model එක Deploy කිරීම

දැන් අපි Python script එකක් ලියලා මුළු deployment process එකම automate කරමු. මේ script එකෙන් වෙන්නේ:

1.  Model එක Vertex AI Model Registry එකට upload කරනවා.
2.  Endpoint එකක් (API URL එකක්) හදනවා.
3.  Model එක ඒ Endpoint එකට connect කරනවා.

**`deploy.py`** ෆයිල් එක හදන්න:

```python
# deploy.py
from google.cloud import aiplatform

# --- Configuration ---
PROJECT_ID = "YOUR_PROJECT_ID"           # ඔයාගේ Project ID එක
BUCKET_NAME = "gs://YOUR-UNIQUE-BUCKET-NAME"  # ඔයාගේ Bucket නම
REGION = "us-central1"

print("🚀 Initializing Vertex AI...")
aiplatform.init(project=PROJECT_ID, location=REGION, staging_bucket=BUCKET_NAME)

# 1. Model එක Registry එකට Upload කිරීම
# අපි පාවිච්චි කරන්නේ Scikit-learn pre-built container එකක්.
print("📦 Uploading model to Vertex AI Registry...")

model = aiplatform.Model.upload(
    display_name="iris-model-v1",
    artifact_uri=BUCKET_NAME,  # model.joblib තියෙන bucket folder එක
    serving_container_image_uri="us-docker.pkg.dev/vertex-ai/prediction/sklearn-cpu.1-0:latest",
)

print(f"✅ Model Uploaded: {model.resource_name}")

# 2. Endpoint එකක් සෑදීම
print("🌐 Creating Endpoint...")
endpoint = aiplatform.Endpoint.create(
    display_name="iris-endpoint",
)

print(f"✅ Endpoint Created: {endpoint.resource_name}")

# 3. Model එක Deploy කිරීම
print("🚀 Deploying model to Endpoint (This takes 10-15 mins)...")
model.deploy(
    endpoint=endpoint,
    deployed_model_display_name="iris-v1",
    machine_type="n1-standard-2",  # Server type එක
    min_replica_count=1,
    max_replica_count=1,
)

print("🎉 Deployment Complete!")
print(f"Endpoint Name: {endpoint.resource_name}")
```

මේක run කරන්න:

```bash
python deploy.py
```

> **වැදගත්:** මේ step එකට විනාඩි 10-20ක් විතර යන්න පුළුවන්. Console එකේ errors අවොත් බලන්න Billing enable ද කියලා.

---

## 7. Method 2: Google Cloud Console (Web UI) භාවිතා කර Deploy කිරීම

ඔයාට Python code ලියන්න අමාරු නම්, මේ ඔක්කොම දේවල් Google Cloud Console website එක හරහා click කරලා කරගන්නත් පුළුවන්.

### Step 1: Model එක Bucket එකට Upload කිරීම

1.  **Google Cloud Console** එකේ දකුණු පැත්තේ menu එකෙන් **Cloud Storage** -> **Buckets** වලට යන්න.
2.  ගියපාර හදපු bucket එක click කරන්න (හෝ උඩ තියෙන "CREATE" button එකෙන් අලුත් එකක් හදන්න).
3.  **"UPLOAD FILES"** button එක click කරලා ඔයාගේ `model.joblib` file එක upload කරන්න.

### Step 2: Vertex AI Model Registry එකට Import කිරීම

1.  Menu එකෙන් **Vertex AI** -> **Model Registry** වලට යන්න.
2.  උඩ තියෙන **"IMPORT"** button එක click කරන්න.
3.  **"Import as new model"** තෝරන්න.
4.  **Name**: මොකක් හරි නමක් දෙන්න (උදා: `iris-model-ui`).
5.  **Region**: `us-central1` (හෝ ඔයාගේ bucket එක තියෙන region එක) තෝරන්න. **CONTINUE** click කරන්න.
6.  **Model Settings**:
    - **Model framework version**: `scikit-learn` තෝරන්න.
    - **Version**: `1.0` (හෝ ඔයාගේ model එකට ගැලපෙන එක).
    - **Pre-built container**: මෙය auto-fill වෙයි.
    - **Model artifact location**: `BROWSE` click කරලා ඔයාගේ bucket එකේ `model.joblib` තියෙන **folder එක** select කරන්න (file එක නෙවෙයි, folder එක).
7.  **IMPORT** click කරන්න.

### Step 3: Endpoint එකක් හදලා Deploy කිරීම

1.  Model එක import වුනාට පස්සේ Model Registry list එකේ ඒක පෙන්නයි. ඒක click කරන්න.
2.  උඩ තියෙන **"DEPLOY TO ENDPOINT"** button එක click කරන්න.
3.  **Define your endpoint**:
    - "Create new endpoint" තෝරන්න.
    - නමක් දෙන්න (උදා: `iris-endpoint-ui`).
    - **CONTINUE** click කරන්න.
4.  **Model settings**:
    - **Traffic split**: 100% දෙන්න.
    - **Machine type**: `n1-standard-2` (හෝ අඩු වියදම් `e2-standard-2`) තෝරන්න.
    - **CONTINUE** -> **DEPLOY** click කරන්න.

විනාඩි 10-15කින් Endpoint එක active වෙයි! ඊට පස්සේ කලින් වගේම `test.py` එකෙන් test කරන්න පුළුවන්.

---

## 8. Test කිරීම

Deployment එක ඉවර වුනාම, අපිට Endpoint එකට data යවලා prediction ගන්න පුළුවන්.

**`test.py`** ෆයිල් එක හදන්න:

```python
# test.py
from google.cloud import aiplatform

PROJECT_ID = "YOUR_PROJECT_ID"
REGION = "us-central1"
ENDPOINT_NAME = "iris-endpoint" # ඔයා කලින් දීපු නම

aiplatform.init(project=PROJECT_ID, location=REGION)

# Endpoint එක හොයාගන්න
endpoints = aiplatform.Endpoint.list(filter=f'display_name="{ENDPOINT_NAME}"')

if not endpoints:
    print("❌ Endpoint not found!")
else:
    endpoint = endpoints[0]
    print(f"✅ Found Endpoint: {endpoint.resource_name}")

    # Test Data (Iris dataset එකේ sample එකක්)
    # [5.1, 3.5, 1.4, 0.2]
    test_instances = [
        [5.1, 3.5, 1.4, 0.2],
        [6.7, 3.0, 5.2, 2.3]
    ]

    print("🔮 Sending prediction request...")
    prediction = endpoint.predict(instances=test_instances)

    print("--- Predictions ---")
    print(prediction.predictions)
```

Run කරන්න:

```bash
python test.py
```

ඔයාට `[0, 2]` වගේ prediction එකක් එනවා නම් වැඩේ හරියටම හරි! 🥳

---

### 🔥 Clean Up (වියදම් අඩු කරගන්න)

වැඩේ ඉවර වුනාම Endpoint එක delete කරන්න අමතක කරන්න එපා, නැත්නම් දිගටම සල්ලි කැපෙනවා.

```python
# python console එකේ ගහන්න
endpoint.undeploy_all()
endpoint.delete()
```
