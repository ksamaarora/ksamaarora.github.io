---
layout: default
title: View Metrics and Evaluate Model with MLflow
---

> #### Review metrics in Azure ML Studio

Open Studio and select your experiment
- In **Details tab**, all **logged parameters** are **shown under** _**Params**_
- Select the **Metrics tab** and select the **metric** you **want to explore**.
- Any **plots** that are **logged** as artifacts can be **found under _Images_**.
- The **model assets** that can be **used to register and deploy** the model are **stored** in the **models folder under _Outputs + logs_**.
  
> #### Retrieve metrics with Mlflow in notebook

[![Screenshot-2024-06-06-at-5-29-18-PM.png](https://i.postimg.cc/g27QRW0R/Screenshot-2024-06-06-at-5-29-18-PM.png)](https://postimg.cc/JsbpVSZ4)
  
- **Search all active experiments** in workspace using Mlflow

```python
experiments = mlflow.search_experiments(max_results=2)
for exp in experiments:
    print(exp.name)
```
  
- **Retrieve archived experiments too**, then include the option _**ViewType.ALL**_

```python
from mlflow.entities import ViewType

experiments = mlflow.search_experiments(view_type=ViewType.ALL)
for exp in experiments:
    print(exp.name)
```
  
- **Retrieve a specific experiment**

```python
exp = mlflow.get_experiment_by_name(experiment_name)
print(exp)
```
  
> #### Retrieve runs

- To search for runs, you **need** either **expt ID or expt name**. E.g. retrieve metrics of a specific run:
```python
mlflow.search_runs(exp.experiment_id)
```
  
- Can also **search across** **all experiments** in workspace using _**search_all_experiments=True**_
  
- By **default**, experiments are **ordered descending** by _**start_time**_, which is **time** the **expt** **was queued in azure ML**. However, you can **change this** default by using the **parameter _order_by_**.

- For example, if you want to **sort by start time** and only **show** the **last two results**:
```python
mlflow.search_runs(exp.experiment_id, order_by=["start_time DESC"], max_results=2)
```
  
- You can also **look for run** with a **specific combination** in the hyperparameters:
```python
mlflow.search_runs(
    exp.experiment_id, filter_string="params.num_boost_round='100'", max_results=2
)
```