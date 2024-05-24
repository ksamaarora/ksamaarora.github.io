---
layout: default
title: Creating Compute Target
---

**When which compute used?**: 
- For **experimentation**: Compute instance or Serverless Spark compute (make use of Spark's distributed compute power)
- For **production**: Compute cluster (automatically scales) or Azure ML Serverless compute
- For **deployment**: 
  - **Batch** predictions - Compute clusters or Azure ML serverless compute
  - **Real-time** predictions - Azure ML containers or Kubernetes cluster

### Create Compute Targets*

### 1) **_Using Python SDK:_**

> ### **Create Compute Instance:** 

A compute instance can be **assigned to one user**, as it **can't handle parallel workloads**. Can **schedule** to start/stop compute instance or **configure** to **automatically shut down** when been **idle** for **set amount** of time

```python
from azure.ai.ml.entities import ComputeInstance

# Compute Instances need to have a unique name across the region.
ci_basic_name = "basic-ci-12345"
ci_basic = ComputeInstance(
    name=ci_basic_name, 
    size="STANDARD_DS3_v2"
)

ml_client.begin_create_or_update(ci_basic).result()
```
> ### **Create a Compute Cluster:**

**3 main parameters** to be defined:
- **_size:_** specify size of VM and also specify u want to use CPU or GPU
- **_max_instances:_** specify maximum number of nodes i.e. the number of parallel workloads compute cluster can handle
- **_tier:_** specify tier of VM - low priority or dedicated

**NOTE:** Increase the **idle time before scale down** to keep the **compute cluster active** between pipeline runs, **minimizing start-up time** for rapid experimentation.

**3 scenarios** to use compute cluster 
- Running a pipeline job you built in the Designer.
- Running an Automated Machine Learning job.
- Running a script as a job.

```python
from azure.ai.ml.entities import AmlCompute

cluster_basic = AmlCompute(
    name="cpu-cluster",
    type="amlcompute",
    size="STANDARD_DS3_v2",
    location="westus",
    min_instances=0,
    max_instances=2,
    idle_time_before_scale_down=120,
    tier="low_priority",
)
ml_client.begin_create_or_update(cluster_basic).result()
```

- **Sample code - set compute target as compute cluster**

```python
from azure.ai.ml import command

# configure job
job = command(
    code="./src",
    command="python diabetes-training.py",
    environment="AzureML-sklearn-0.24-ubuntu18.04-py37-cpu@latest",
    compute="cpu-cluster",
    display_name="train-with-cluster",
    experiment_name="diabetes-training"
    )

# submit job
returned_job = ml_client.create_or_update(job)
aml_url = returned_job.studio_url
print("Monitor your job at", aml_url)
```

### 2) **_Using Azure CLI:_***

> ### **Create Compute Instance** 

- Settings:
  - **Compute name:** Name of compute instance. Has to be unique and fewer than 24 characters.
  - **Virtual machine size:** STANDARD_DS11_V2
  - **Compute type (instance or cluster):** ComputeInstance
  - **Azure Machine Learning workspace name:** mlw-dp100-labs
  - **Resource group:** rg-dp100-labs

```bash
az ml compute create --name "ci1572" --size STANDARD_DS11_V2 --type ComputeInstance -w mlw-dp100-labs -g rg-dp100-labs
```

> ### **Create Compute Cluster**

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

> ### **Create compute target**

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
