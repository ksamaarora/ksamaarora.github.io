---
layout: post
title:  "How to Deploy Machine Learning Models with Azure Machine Learning"
date:   2024-12-11 09:29:20 +0700
tags:
  - cloud
categories: jekyll update
usemathjax: true
---

**How to Deploy Machine Learning Models with Azure Machine Learning**

With machine learning gaining popularity, many businesses are adding machine learning models to existing systems. Model deployment integrates a machine learning model into a production environment. If done well, this empowers businesses to make data-driven decisions in weeks. Knowledge of efficient model deployment is an essential skill for competitive data scientists.

### Contents

- [What is Azure Machine Learning?](#what-is-azure-machine-learning)
- [Step 1: Register Your Model](#1-register-your-model)
- [Step 2: Prepare to Deploy](#2-prepare-to-deploy)
- [Step 3: Deploy to Target](#3-deploy-to-target)
- [Step 4: Consume Web Services](#4-consume-web-services)

### What is Azure Machine Learning?

Azure Machine Learning is a cloud service that helps you train, deploy, automate, and manage machine learning models at scale. It fully supports open-source technologies such as PyTorch, TensorFlow, and scikit-learn. 

[![Screenshot-2024-12-12-at-6-15-19-PM.png](https://i.postimg.cc/NGPrQTC2/Screenshot-2024-12-12-at-6-15-19-PM.png)](https://postimg.cc/t7Wg51j9)

Efficient deployment of machine learning models is essential for businesses to integrate data-driven decisions into their systems. 

**Note:** The deployment workflow is similar regardless of where you deploy your model.

### 1. Register Your Model

First, register your machine learning model in your Azure Machine Learning workspace. You can register a model either from an **Experiment Run** or from an **externally created model**.

- **Register a model from an Experiment Run**: 

  - Scikit-learn example using the SDK:
    ```python
    model = run.register_model(model_name='sklearn_mnist', model_path='outputs/sklearn_mnist_model.pkl')
    print(model.name, model.id, model.version, sep='\t')
    ```

  - Using the CLI:
    ```bash
    az ml model register -n sklearn_mnist --asset-path outputs/sklearn_mnist_model.pkl --experiment-name myexperiment
    ```

  - Using VS Code: Register models using any model files or folders with the Visual Studio Code extension.

- **Register an externally created model**: If the model was created outside Azure, you can register it by providing a local path to the model (folder or single file).

  - ONNX example with the Python SDK:
    ```python
    import urllib.request
    onnx_model_url = "https://www.cntk.ai/OnnxModels/mnist/opset_7/mnist.tar.gz"
    urllib.request.urlretrieve(onnx_model_url, filename="mnist.tar.gz")
    !tar xvzf mnist.tar.gz

    model = Model.register(workspace=ws,
                           model_path="mnist/model.onnx",
                           model_name="onnx_mnist",
                           tags={"onnx": "demo"},
                           description="MNIST image classification CNN from ONNX Model Zoo")
    ```

  - Using the CLI:
    ```bash
    az ml model register -n onnx_mnist -p mnist/model.onnx
    ```

### 2. Prepare to Deploy

To deploy a model as a web service, create an **inference configuration** (_InferenceConfig_) and a **deployment configuration**. The entry script receives data submitted to a deployed web service, passes it to the model, and returns the response to the client.

The script contains two functions:
- **_init()_**: Loads the model into a global object when the Docker container starts (runs only once).
- **_run(input_data)_**: Uses the model to predict values based on the input data.

### 3. Deploy to Target

To deploy the model, configure the deployment based on your target compute resource, such as local machines, Azure Container Instances (ACI), or Azure Kubernetes Services (AKS).

[![Screenshot-2024-12-12-at-6-41-06-PM.png](https://i.postimg.cc/zfr93xXd/Screenshot-2024-12-12-at-6-41-06-PM.png)](https://postimg.cc/xX6s4ymH)

Below is an example using an existing AKS cluster with the Azure Machine Learning SDK, CLI, or the Azure portal:

- Using the SDK:
    ```python
    aks_target = AksCompute(ws, "myaks")

    deployment_config = AksWebservice.deploy_configuration(cpu_cores=1, memory_gb=1)

    service = Model.deploy(ws, "aksservice", [model], inference_config, deployment_config, aks_target)

    service.wait_for_deployment(show_output=True)

    print(service.state)
    print(service.get_logs())
    ```

- Using the CLI:
    ```bash
    az ml model deploy -ct myaks -m mymodel:1 -n aksservice -ic inferenceconfig.json -dc deploymentconfig.json
    ```

- Using VS Code: Deploy to AKS via the VS Code extension, configuring AKS clusters in advance.

### 4. Consume Web Services

Every deployed web service provides a REST API, allowing you to create client applications in various programming languages. If authentication is enabled for your service, include a service key as a token in the request header.

Example of invoking the service in Python:
```python
import requests
import json

headers = {'Content-Type': 'application/json'}

if service.auth_enabled:
    headers['Authorization'] = 'Bearer ' + service.get_keys()[0]

test_sample = json.dumps({'data': [
    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
    [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
]})

response = requests.post(service.scoring_uri, data=test_sample, headers=headers)

print(response.status_code)
print(response.elapsed)
print(response.json())
```

The general workflow to create a client that uses a machine learning web service involves:
1. Using the SDK to get the connection information.
2. Determining the type of request data used by the model.
3. Creating an application that calls the web service.

--- 