---
layout: default
title: Optimize Hyperparameters
---

> ### **Steps to Optimize Hyperparameters:**

> **Step 1: Define Parameter Search Space**:
   - Specify batch size and number of hidden layers 

```python
{
    "batch_size": choice(1, 2, 3, 4)
    "number_of_hidden_layers": choice(range(1,5))
}
```

```python
from azureml.train.hyperdrive import GridParameterSampling
from azureml.train.hyperdrive import choice

param_sampling = GridParameterSampling({
        "num_hidden_layers": choice(1, 2, 3),
        "batch_size": choice (16, 32)
    }
)
```
   
> **Step 2: Specify Primary Metric**:
   - Choose a primary metric to optimize, such as accuracy.

```python
primary_metric_name="accuracy",
primary_metric_goal=PrimaryMetricGoal.MAXIMIZE
```

> **Step 3: Specify Early Termination Policy**:
   - Select a policy to stop low-performing runs early.

```python
from azureml.train.hyperdrive import BanditPolicy

early_termination_policy = BanditPolicy 
        (slack_factor = 0.1, evaluation_interval=1, delay_evaluation=5)
```

> **Step 4: Create and Assign Resources**:
   - Allocate computational resources for the experiment.
```python 
max_total_runs=20,
max_concurrent_runs=4
```

> **Step 5: Launch Experiment**:
   - Run the experiment with the defined configuration.

> **Step 6: Visualize Training Runs**:
   - Analyze the performance of different runs to understand the results.
[![Screenshot-2024-05-16-at-11-03-55-PM.png](https://i.postimg.cc/tCZ7ZB53/Screenshot-2024-05-16-at-11-03-55-PM.png)](https://postimg.cc/4mGXjbjy)

> **Step 7: Select Best Configuration**:
   - Choose the hyperparameter configuration that yields the best performance.


