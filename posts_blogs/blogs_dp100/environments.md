---
layout: default
title: Azure Machine Learning Environments
---

> #### IMP Note: Environment OS and Azure Container Registry are two properties of Azure ML environments definitions. 

**List environments** in studio, using Azure CLI or Python SDK
Using Python SDK
```python
envs = ml_client.environments.list()
for env in envs:
    print(env.name)
```

**Review details** of an environment by its registered name
```python
env = ml_client.environments.get(name="my-environment", version="1")
print(env)
```

Use environment when you want to **run a script** as a **(command) job**
For example, following code shows how to **configure a command job** with the **Python SDK**, which uses a **curated environment** including Scikit-Learn:

```python
from azure.ai.ml import command

# configure job
job = command(
    code="./src",
    command="python train.py",
    environment="AzureML-sklearn-0.24-ubuntu18.04-py37-cpu@latest",
    compute="aml-cluster",
    display_name="train-with-curated-environment",
    experiment_name="train-with-curated-environment"
)

# submit job
returned_job = ml_client.create_or_update(job)
```

- If **job fails**, review the detailed errors in **_Output + logs_** tab of your job and a **common error message** that indicates env is incomplete, is **_ModuleNotFoundError_**. 

### Create and use custom environments

- **Create environment from docker image**

Docker images can be hosted in a public registry like **_Docker Hub_** or privately stored in Azure Container registry. Many open-source frameworks are encapsulated in public images to be found in Docker Hub. 

```python
from azure.ai.ml.entities import Environment

env_docker_image = Environment(
    image="pytorch/pytorch:latest",
    name="public-docker-image-example",
    description="Environment created from a public Docker image.",
)
ml_client.environments.create_or_update(env_docker_image)
```

- **Create environment using Azure ML base images**

```python
from azure.ai.ml.entities import Environment

env_docker_image = Environment(
    image="mcr.microsoft.com/azureml/openmpi3.1.2-ubuntu18.04",
    name="aml-docker-image-example",
    description="Environment created from a Azure ML Docker image.",
)
ml_client.environments.create_or_update(env_docker_image)
```

- **Create a custom environment with a conda specification file**

Though docker image contains all necessary packages, if needed to **include other packages** to run code, **add the conda specification file** to Docker image when creating environment. 
A conda specification file is a **YAML file**, which **lists all the packages** that **needs to be installed** using **_conda_** or **_pip_**. 

- Sample of a YAML file

```yaml
name: basic-env-cpu
channels:
  - conda-forge
dependencies: # important
  - python=3.7 #python packages
  - scikit-learn 
  - pandas
  - numpy
  - matplotlib
```

- **Create environment from base Docker image and conda specialization file**

```python
from azure.ai.ml.entities import Environment

env_docker_conda = Environment(
    image="mcr.microsoft.com/azureml/openmpi3.1.2-ubuntu18.04",
    conda_file="./conda-env.yml",
    name="docker-image-plus-conda-example",
    description="Environment created from a Docker image plus Conda environment.",
)
ml_client.environments.create_or_update(env_docker_conda)
```

**Note:** When Azure ML builds an environment, its **added to the list of custom environments** in the workspace. The **image of the env** is **hosted** in the **Azure Container registry** associated to the workspace. Use the same env next time, **no need to build again**. 

