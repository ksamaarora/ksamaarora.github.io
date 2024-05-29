---
layout: default
title: Sample codes for Sampling Methods
---

### Sample codes for Sampling Methods:

> ### Grid Sampling:
  
  E.g. Grid Sampling is used to try every possible combination of discrete batch_size and learning_rate value: 

  ```python
  from azure.ai.ml.sweep import Choice
  
  command_job_for_sweep = command_job(
      batch_size=Choice(values=[16, 32, 64]),
      learning_rate=Choice(values=[0.01, 0.1, 1.0]),
  )
  
  sweep_job = command_job_for_sweep.sweep(
      sampling_algorithm = "grid",
      ...
  )
  ```
  
> ### Random Sampling: 

  ```python
  from azure.ai.ml.sweep import Normal, Uniform
  
  command_job_for_sweep = command_job(
      batch_size=Choice(values=[16, 32, 64]),   
      learning_rate=Normal(mu=10, sigma=3),
  )
  
  sweep_job = command_job_for_sweep.sweep(
      sampling_algorithm = "random",
      ...
  )
  ```
  
> ### Sobol

The following code example shows how to use Sobol by adding a seed and a rule, and using the _**RandomSamplingAlgorithm**_ class:

  ```python
  from azure.ai.ml.sweep import RandomSamplingAlgorithm
  
  sweep_job = command_job_for_sweep.sweep(
      sampling_algorithm = RandomSamplingAlgorithm(seed=123, rule="sobol"),
      ...
  )
  ```
  
> ### Bayesian Sampling

The following code example shows how to configure Bayesian sampling:

  ```python
  from azure.ai.ml.sweep import Uniform, Choice
  
  command_job_for_sweep = job(
      batch_size=Choice(values=[16, 32, 64]),    
      learning_rate=Uniform(min_value=0.05, max_value=0.1),
  )
  
  sweep_job = command_job_for_sweep.sweep(
      sampling_algorithm = "bayesian",
      ...
  )
  ```