---
layout: default
title: Track ML Jobs with Mlflow
---

> #### Enable autologging

- **Automatically logs parameters**, **metrics**, and **model artifacts** **without** anyone **needing** to **specify** what needs to be **logged**.
- Supported by
    • **Scikit-learn**
    • **TensorFlow** and **Keras**
    • **XGBoost**
    • **Light GBM**
    • **Spark**
    • **Fastai**
    • **Pytorch**

- **To enable autologging**, add following code for training script

```python
import mlflow

mlflow.autolog()
```
  
> #### Log Metrics with Mlflow i.e. Use logging functions to track custom metrics using mlflow
  
- Can decide whatever custom metric u want to log with MLflow

- _**mlflow.log_param(my_custom_param)**_: **Log single key-value parameter**. Use this function for an **input parameter** you want **to** **log**.
- _**mlflow.log_metric(my_custom_metric)**_: Log **single key-value metric**. Value must be a **number**. Use this function for **any output** you want to **store** with the run.
- _**mlflow.log_artifact(my_custom_artifact)**_: **Log a file**. Use this function for **any plot** you want to log, **save as image file first**.

- **Sample code to add Mlflow** to an existing training script:

```python
import mlflow
  
reg_rate = 0.1
mlflow.log_param("Regularization rate", reg_rate)
```

- Finally **submit** the job