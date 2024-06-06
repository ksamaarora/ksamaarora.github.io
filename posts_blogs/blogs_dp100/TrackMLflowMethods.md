---
layout: default
title: Track ML Jobs with Mlflow
---

[![Screenshot-2024-06-04-at-1-35-36-AM.png](https://i.postimg.cc/MHGK70BN/Screenshot-2024-06-04-at-1-35-36-AM.png)](https://postimg.cc/r0vkcrQN)

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

- **To enable autologging** (feature that **logs all parameters, metrics and artfacts**, **without** needing to specifically **set up** those logs)

```python
import mlflow

mlflow.autolog()
```
  
> #### Log Metrics with Mlflow i.e. Use logging functions to track custom metrics using mlflow
  
- Can decide whatever custom metric u want to log with MLflow

> ### IMP NOTE:
- _**mlflow.log_param(my_custom_param)**_: **Log single key-value parameter**. Used to **log parameters** such as **hyper parameters**. Use this function for an **input parameter** you want **to** **log**.
- _**mlflow.log_metric(my_custom_metric)**_: Log **single key-value metric**. Value must be a **number**. **Used to log metrics like accuracy**. Use this function for **any output** you want to **store** with the run.
- _**mlflow.log_artifact(my_custom_artifact)**_: **Log a file**. Use this function for **any plot** you want to log, **save as image file first**.

- **Sample code to add Mlflow** to an existing training script:

```python
import mlflow
  
reg_rate = 0.1
mlflow.log_param("Regularization rate", reg_rate)
```

- Finally **submit** the job

[![Screenshot-2024-06-04-at-1-36-23-AM.png](https://i.postimg.cc/Dwhf5K11/Screenshot-2024-06-04-at-1-36-23-AM.png)](https://postimg.cc/QH6rxw4M)