---
layout: default
title: Training Model by using Python SDK
---

### Training Model by using Python SDK

> Step 1 - **Connect to Workspace**:

```python
from azure.identity import DefaultAzureCredential, InteractiveBrowserCredential 
from azure.ai.ml import MLClient

try:
    credential = DefaultAzureCredential()
    # Check if given credential can get token successfully.
    credential.get_token ("https://management.azure.com/.default")
except Exception as ex:
    # Fall back to InteractiveBrowserCredential in case DefaultAzureCredential not work 
    credential = InteractiveBrowserCredential()
```

```python
# Get a handle to workspace
ml_client = MLClient.from_config(credential=credential)
```

> Step 2 - **Use Python SDK to train model** (Here creating a regression model to predict diabetes)

```python
%%writefile src/diabetes-training.py
# import libraries 
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split 
from sklearn.linear_model import LogisticRegression 
from sklearn.metrics import roc_auc_score
from sklearn.metrics import roc_curve

# load the diabetes dataset
print("Loading Data...")
diabetes = pd.read_csv('diabetes.csv')

# separate features and labels
X, y = diabetes [['Pregnancies', 'PlasmaGlucose', 'DiastolicBlood Pressure', 'Triceps Thickness', 'SerumInsulin', 'BMI', 'Diabetes Pedigree', 'Age']

# split data into training set and test set
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.30, random_state=0)

# set regularization hyperparameter
reg = 0.01

# train a logistic regression model
print('Training a logistic regression model with regularization rate of', reg)
model = LogisticRegression (C=1/reg, solver="liblinear").fit(X_train, y_train)

# calculate accuracy
y_hat = model.predict(X_test)
acc = np.average (y_hat == y_test) 
print('Accuracy:', acc)

# calculate AUC
y_scores = model.predict_proba (X_test) 
auc = roc_auc_score (y_test,y_scores [:,1]) 
print('AUC: ' + str(auc))
```
> Step 3 - **Submit the job** 

```python
from azure.ai.ml import command

# configure job 
job = command (
    code="./src",
    command="python diabetes-training.py",
    environment="AzureML-sklearn-0.24-ubuntu18.04-py37-cpu@latest",
    compute="aml-cluster",
    display_name="diabetes-pythonv2-train", 
    experiment_name="diabetes-training"
)

# submit job
returned_job = ml_client.create_or_update (job)
aml_url = returned_job.studio_url
print("Monitor your job at", aml_url)
```