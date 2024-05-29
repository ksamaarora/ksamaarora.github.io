---
layout: default
title: Use a sweep job for hyperparameter tuning
---

### Use a sweep job for hyperparameter tuning

> ### Create training script for hyperparameter tuning:

**Script** must include **argument** for each hyperparameter and **log target performance metric with Mlflow**. A logged metric enables the sweep job to evaluate performance of trials it initiates, and identifies the one that produces the best performing model. 
  
Sample script training a logistic regression model using a **_--regularization_** argument to set the regularization rate hyperparameter, and logs the accuracy metric with the name _**Accuracy**_
  
**Note:** Use **mlflow.log_metric()** statement to **log the AUC value** i.e. to train a model based on **target metric** named "AUC", say. 
  
```python
import argparse
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
import mlflow
  
# get regularization hyperparameter
parser = argparse.ArgumentParser()
parser.add_argument('--regularization', type=float, dest='reg_rate', default=0.01)
args = parser.parse_args()
reg = args.reg_rate
  
# load the training dataset
data = pd.read_csv("data.csv")
  
# separate features and labels, and split for training/validatiom
X = data[['feature1','feature2','feature3','feature4']].values
y = data['label'].values
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.30)
  
# train a logistic regression model with the reg hyperparameter
model = LogisticRegression(C=1/reg, solver="liblinear").fit(X_train, y_train)
  
# calculate and log accuracy
y_hat = model.predict(X_test)
acc = np.average(y_hat == y_test)
mlflow.log_metric("Accuracy", acc)
```
  
> ### Configure and run sweep job 

- Create base command that specifies which script to run and defines parameters used by script

```python
from azure.ai.ml import command
    
# configure command job as base
job = command(
    code="./src",
    command="python train.py --regularization ${{inputs.reg_rate}}",
    inputs={
        "reg_rate": 0.01,
    },
    environment="AzureML-sklearn-0.24-ubuntu18.04-py37-cpu@latest",
    compute="aml-cluster",
    )
```

- Then override input parameters with search space

```python
from azure.ai.ml.sweep import Choice
    
command_job_for_sweep = job(
    reg_rate=Choice(values=[0.01, 0.1, 1]),
)
```

- Call sweep() on your command job to sweep search space 

```python
from azure.ai.ml import MLClient
    
# apply the sweep parameter to obtain the sweep_job
sweep_job = command_job_for_sweep.sweep(
    compute="aml-cluster",
    sampling_algorithm="grid",
    primary_metric="Accuracy",
    goal="Maximize",
)
    
# set the name of the sweep job experiment
sweep_job.experiment_name="sweep-example"
    
# define the limits for this sweep
sweep_job.set_limits(max_total_trials=4, max_concurrent_trials=2, timeout=7200)
    
# submit the sweep
returned_sweep_job = ml_client.create_or_update(sweep_job)
```
  
> ### Lastly monitor and review sweep jobs 