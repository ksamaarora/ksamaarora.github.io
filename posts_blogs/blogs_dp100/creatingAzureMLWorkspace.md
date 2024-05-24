---
layout: default
title: Creating Azure ML Workspace
---

> #### Access in Azure ML Workspace*

- Access is granted in Azure using **role-based access control (RBAC)**, which can configure Access control tab of resource or resource group. You can manage permissions to restrict what actions certain users or teams can perform **3 built-in roles** you can use across resources and resource groups to assign permissions to other users:
  - **Owner:** Gets **full access** to all resources, and **can grant access** to others using access control.
  - **Contributor:** Gets **full access** to all resources, but **can't grant** access to others.
  - **Reader:** Can **only view** the resource, but **isn't allowed** to make any **changes**.
- Additionally, **Azure ML** has specific **built-in roles** you can use:
  - **AzureML Data Scientist:** Can **perform all actions** within the workspace, **except** for **creating or deleting compute resources**, or **editing** the **workspace settings**.
  - **AzureML Compute Operator:** Is allowed to **create, change, and manage access** the compute resources within a workspace.

> #### **_Using Python SDK to interact with Azure ML workspace_***
  - **Install Python SDK:**
  ```python
  pip install azure-ai-ml
  ```
  - **Connect to Workspace**: We **authenticate** the **MLClient** is used to connect to the workspace. To authenticate, we need **3 parameters** - subscription_id, resource_group and workspace_name
```python
from azure.ai.ml import MLClient
from azure.identity import DefaultAzureCredential
ml_client = MLClient(
    DefaultAzureCredential(), subscription_id, resource_group, workspace
)
```
  - **Create New Machine Learning Workspace**
```python
from azureml.core import Workspace
my_ws = Workspace(
    name="another-workspace",
    location="westus",
    display_name="another-workspace for you to view", 
    description="This is just an example"
)
ml_client.workspaces.begin_create(my_ws)
```
  - **Sample code to configure and run a job**
```python
from azure.ai.ml import command
# configure job
job = command(
    code="./src",
    command="python train.py",
    environment="AzureML-sklearn-0.24-ubuntu18.04-py37-cpu@latest",
    compute="aml-cluster",
    experiment_name="train-model"
)
# connect to workspace and submit job
returned_job = ml_client.create_or_update(job)
# Print the URL to monitor the job
aml_url = returned_job.studio_url
print("Monitor your job at", aml_url)
```

> **_Using Azure CLI to interact with Azure ML workspace_**
- **Remove any ML CLI extensions** (Both version 1 and 2) to avoid conflicts with previous versions 
```bash
  az extension remove -n azure-cli-ml 
  az extension remove -n ml
```
- **Install** Azure ML (v2) extension 
```bash
az extension add -n ml -y
```
- **Create resource group** and choose a location close to you
```bash
az group create --name "rg-dp100-labs" --location "eastus"
```
- **Create a workspace**
```bash
az ml workspace create --name "mlw-dp100-labs" -g "rg-dp100-labs"
```
- Wait for workspace and associated resources to be created 
