---
layout: default
title: Managed Online Endpoint without Mlflow
---

### (II) DEPLOY MODEL TO A MANAGED ONLINE ENDPOINT WITHOUT USING Mlflow MODEL FORMAT

**To deploy model**, you must create:
  - **Model files** stored on local path or registered model. The model files can be logged and stored when you train a model
  - **A scoring script** (**Not automatically created** like MLflow model deployment)
  - **An execution environment** ("")
  - **Compute configuration** for deployment
    - **instance_type:** VM size to use
    - **instance_count:** Number of instances to use


> #### (A) Create a scoring script:

**Scoring script needs to include two functions:**
  - **init():** Called when the **service is intialized**
  - **run():** Called when **new data** is **submitted to** the **service**
  
```python
import json
import joblib
import numpy as np
import os

# init function is called when the deployment is created or updated, to load and cache the model from the model registry

def init():
    global model
    # get the path to the registered model file and load it
    model_path = os.path.join(os.getenv('AZUREML_MODEL_DIR'), 'model.pkl')
    model = joblib.load(model_path)

# run function is called for every time the endpoint is invoked (called when a request is received), to generate predictions from the input data  

def run(raw_data):
    # get the input data as a numpy array
    data = np.array(json.loads(raw_data)['data'])
    # get a prediction from the model
    predictions = model.predict(data)
    # return the predictions as any JSON serializable format
    return predictions.tolist()
```

> #### (B) Create an environment

**Can create with base Docker image, and define Conda dependencies in conda.yml file**

- **YML file code**

```yml
name: basic-env-cpu
channels:
  - conda-forge
dependencies:
  - python=3.7
  - scikit-learn
  - pandas
  - numpy
  - matplotlib
```

**Code to create environment with yml file** 

```python
from azure.ai.ml.entities import Environment

env = Environment(
    image="mcr.microsoft.com/azureml/openmpi3.1.2-ubuntu18.04",
    conda_file="./src/conda.yml",
    name="deployment-environment",
    description="Environment created from a Docker image plus Conda environment.",
)
ml_client.environments.create_or_update(env)
```

> ### Create deployment

**To deploy the model, use the ManagedOnlineDeployment class:**

```python
from azure.ai.ml.entities import ManagedOnlineDeployment, CodeConfiguration

model = Model(path="./model",

blue_deployment = ManagedOnlineDeployment(
    name="blue",
    endpoint_name="endpoint-example",
    model=model,
    environment="deployment-environment",
    code_configuration=CodeConfiguration(
        code="./src", scoring_script="score.py"
    ),
    instance_type="Standard_DS2_v2",
    instance_count=1,
)

ml_client.online_deployments.begin_create_or_update(blue_deployment).result()
```

**Can deploy multiple models to an endpoint. To direct traffic to a specific deployment:**
```python
# blue deployment takes 100 traffic
endpoint.traffic = {"blue": 100}
ml_client.begin_create_or_update(endpoint).result()
```

**To delete endpoint and all associated deployments** 
```python
ml_client.online_endpoints.begin_delete(name="endpoint-example")
```