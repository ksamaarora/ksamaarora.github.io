---
layout: default
title: Managed Online Endpoint
---

### (I) DEPLOY MLFLOW MODEL TO A MANAGED ONLINE ENDPOINT

**Note:** When you **deploy MLFlow models to an online endpoint**, **a scoring script and environment** are **automatically generated**, and **no need to create** them.

**To deploy Mlflow model**, you need 
  - **Model files** stored **on a local path** OR **with registered models** 
  - **Compute configuration** for deployment 
    ○ **instance_type:** VM size to use
    ○ **instance_count:** Number of instances to use

> **Code to deploy a MLflow model to managed online endpoint:**

```python
from azure.ai.ml.entities import Model, ManagedOnlineDeployment
from azure.ai.ml.constants import AssetTypes

# create a blue deployment
model = Model(
    path="./model",
    type=AssetTypes.MLFLOW_MODEL,
    description="my sample mlflow model",
)

blue_deployment = ManagedOnlineDeployment(
    name="blue",
    endpoint_name="endpoint-example",
    model=model,
    instance_type="Standard_F4s_v2",
    instance_count=1,
)

ml_client.online_deployments.begin_create_or_update(blue_deployment).result()
```

> **Deploy to a specific model among mutiple models: (IMP)** 

Since **only one model deployed**, **100%** of traffic is to this model. However **if multiple models are deployed** to same endpoint, and to direct traffic to a specific deployment use this code
```python
# blue deployment takes 100 traffic
endpoint.traffic = {"blue": 100}
ml_client.begin_create_or_update(endpoint).result()
```

**IMP NOTE:** **25%** traffic goes to **blue model** and **75%** goes to **green model**. Code snippet implementing desired blue/green configuration:

```python
endpoint.traffic = {"blue": 25, "green": 75} 
ml_client.begin_create_or_update(endpoint).result()
```

> **To delete endpoint and all associated deployments**
 
```python
ml_client.online_endpoints.begin_delete(name="endpoint-example")
```