---
layout: default
title: Creating Compute Target
---

> ### Create Compute Targets

> **_Using Python SDK:_**
  - Create **Compute instance**
```python
# Compute Instances need to have a unique name across the region.
# Here we create a unique name with current datetime
from azure.ai.ml.entities import ComputeInstance, AmlCompute
ci_basic_name = "basic-ci"
ci_basic = ComputeInstance(name=ci_basic_name, size="STANDARD_DS3_v2")
ml_client.begin_create_or_update(ci_basic)
```
  - Create **Compute cluster:** Specify **size and min max instances** required. This means when the VM is **idle** it ill resize to **min instances** and whenever in use it will scale up to max instances. 
```python
from azure.ai.ml.entities import AmlCompute
cluster_basic = AmlCompute(
name="basic-example",
type="amlcompute",
size="STANDARD_DS3_v2",
location="westus",
min_instances=0,
max_instances=2,
idle_time_before_scale_down=120,
)
ml_client.begin_create_or_update(cluster_basic)
```

> **_Using Azure CLI:_***
- **_Create Compute instance using Azure CLI_** 
  - Settings:
    - **Compute name:** Name of compute instance. Has to be unique and fewer than 24 characters.
    - **Virtual machine size:** STANDARD_DS11_V2
    - **Compute type (instance or cluster):** ComputeInstance
    - **Azure Machine Learning workspace name:** mlw-dp100-labs
    - **Resource group:** rg-dp100-labs
```bash
az ml compute create --name "ci1572" --size STANDARD_DS11_V2 --type ComputeInstance -w mlw-dp100-labs -g rg-dp100-labs
```
- **_Create compute cluster with Azure CLI_**
  - Settings
    - **Compute name:** aml-cluster
    - **Virtual machine size:** STANDARD_DS11_V2
    - **Compute type:** AmlCompute (Creates a compute cluster)
    - **Maximum instances:** Maximum number of nodes
    - **Azure Machine Learning workspace name:** mlw-dp100-labs
    - **Resource group:** rg-dp100-labs
```bash
az ml compute create --name "aml-cluster" --size STANDARD_DS11_V2 --max-instances 2 --type AmlCompute -w mlw-dp100-labs -g rg-dp100-labs
```
- **_Create compute target_**
  ```bash
  az ml compute create --name aml-cluster --size STANDARD_DS3_v2 --min-instances 0 --max-instances 5 --type AmlCompute --resource-group my-resource-group --workspace-name my-workspace
  ```
- Can use **YAML files** to **define configuration** - becomes easier to organize and automate tasks
  - **NOTE:** Designed for **automating tasks**. By using YAML files to define how the **model must be trained**, the **ML tasks** will be **repeatable**, **consistent** and **reliable**.
```yml
  $schema: https://azuremlschemas.azureedge.net/latest/amlCompute.schema.json 
  name: aml-cluster
  type: amlcompute
  size: STANDARD_DS3_v2
  min_instances: 0
  max_instances: 5
```
- When u saved the YAML file as compute.yml, you can create compute target by following command
```bash
  az ml compute create --file compute.yml --resource-group my-resource-group --workspace-name my-workspace
```
