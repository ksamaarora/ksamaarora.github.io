---
layout: default
title: Training Model by using Python SDK
---

### Training Model by using Python SDK

[![Screenshot-2024-05-17-at-2-04-40-AM.png](https://i.postimg.cc/y8Bc2Sdr/Screenshot-2024-05-17-at-2-04-40-AM.png)](https://postimg.cc/0bWzwj7p)

[![Screenshot-2024-05-17-at-2-05-13-AM.png](https://i.postimg.cc/RZX68s2N/Screenshot-2024-05-17-at-2-05-13-AM.png)](https://postimg.cc/CRnxnNhg)

[![Screenshot-2024-05-17-at-2-05-34-AM.png](https://i.postimg.cc/MTyWkXXd/Screenshot-2024-05-17-at-2-05-34-AM.png)](https://postimg.cc/JDzwZrNk)

## Run Training Script as Command Job in Azure Ml

### Step 1: Convert a Notebook to a Script

Scripts are ideal for testing and automation in production. To create a production-ready script:
- **Remove nonessential code**: Exclude unnecessary code like _**print()**_ and _**df.describe()**_ (i.e. code for exploratory purposes) to reduce costs and compute time.
- **Refactor into functions**: Break down the code into smaller functions to test parts of the code independently resulting in run of only the required part of code.

Example notebook code to read and split data:

```python
# read and visualize the data
print("Reading data...")
df = pd.read_csv('diabetes.csv')
df.head()

# split data
print("Splitting data...")
X, y = df[['Pregnancies','PlasmaGlucose','DiastolicBloodPressure','TricepsThickness','SerumInsulin','BMI','DiabetesPedigree','Age']].values, df['Diabetic'].values

from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.30, random_state=0)
```

**Refactored into two functions** - Read the data & Split the data:
- **Note:** A **script** consisting of **multiple functions** is **best** to use for **production workloads**. **E.g.** A data scientist has trained a model in a notebook. The model should be retrained every week on new data.

```python
def main(csv_file):
    df = get_data(csv_file)

    # Split data
    X_train, X_test, y_train, y_test = split_data(df)

# function that reads the data
def get_data(path):
    df = pd.read_csv(path)
    return df

# function that splits the data
def split_data(df):
    X, y = df[['Pregnancies','PlasmaGlucose','DiastolicBloodPressure','TricepsThickness','SerumInsulin','BMI','DiabetesPedigree','Age']].values, df['Diabetic'].values
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.30, random_state=0)
    return X_train, X_test, y_train, y_test
```

**Test the script in the terminal:**
- Open notebook page of Azure ML Studio -> save and run script in terminal
- **OR**
- Go to compute page -> select terminal of compute instance -> use command to run python script named _train.py_
```sh
python train.py
```

### Step 2: Run a Script as a Command Job

Configure and submit a command job with Python SDK (v2):
- **code**: Folder containing the script.
- **command**: Specifies the file to run.
- **environment**: Required packages.
- **compute**: Compute resource.
- **display_name**: Job name.
- **experiment_name**: Experiment name.

Example configuration:

```python
from azure.ai.ml import command

job = command(
    code="./src",
    command="python train.py",
    environment="AzureML-sklearn-0.24-ubuntu18.04-py37-cpu@latest",
    compute="aml-cluster",
    display_name="train-model",
    experiment_name="train-classification-model"
)

# Submit job
returned_job = ml_client.create_or_update(job)
```

### Step 3: Use Parameters in Command Job

Increase script flexibility using parameters.

**Using script arguments**:
```python
import argparse # using library argparse
import pandas as pd
from sklearn.linear_model import LogisticRegression

def main(args):
    # read data
    df = get_data(args.training_data)

# function that reads the data
def get_data(path):
    df = pd.read_csv(path)
    return df

def parse_args():
    # setup arg parser
    parser = argparse.ArgumentParser()

    # add arguments
    parser.add_argument("--training_data", dest='training_data', type=str)

    # parse args
    args = parser.parse_args()

    # return args
    return args

# run script
if __name__ == "__main__":

    # parse args
    args = parse_args()

    # run main function
    main(args)
```

**Passing arguments to a script**:
```sh
python train.py --training_data diabetes.csv
```

**Configure command job with arguments:**
```python
from azure.ai.ml import command

job = command(
    code="./src",
    command="python train.py --training_data diabetes.csv",
    environment="AzureML-sklearn-0.24-ubuntu18.04-py37-cpu@latest",
    compute="aml-cluster",
    display_name="train-model",
    experiment_name="train-classification-model"
)
```


<!-- GIVEN IN CLOUD GURU -->
<!-- > Step 1 - **Connect to Workspace**:

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
``` -->