---
layout: default
title: Anaconda Jupyter
---
> ## Anaconda

Anaconda is an open-source distribution of the Python and R programming languages for data science, machine learning, and scientific computing. To start Anaconda, type **_python_** in iTerm. To exit python, write **exit()**.

### Anaconda Pkg Management

- **__pip list_**: to list all pkgs
- **_conda --help_**
- **_conda list_**: list all installed pkgs

### Conda Environments

- **_conda create --name my_app flask sqlalchemy_**: create new env named "my_app" with specific packages.
  - **_source activate my_app_**: to activate the env
  - **_source deactivate_**: to deactivate the env

### Managing Environments

- **_conda env list_**: to view list of env created
- To remove an env, use **_conda remove --name my_app --all_** (using **_--all_** removes all packages in that environment)

> ## Jupyter Notebook Quick Reference 

In Jupyter Notebook, there are two primary modes: **Command Mode** and **Edit Mode**.

**Magic Commands** enhance the functionality of Jupyter Notebooks. Commands prefixed with % are **line magics** and are applied to a single line, while those prefixed with %% are **cell magics** and are applied to the entire cell. 

Line magics include useful commands like **_%lsmagic, %pwd, %ls -la, %matplotlib inline_**. Cell magics include commands like **_%%HTML, %%javascript, %%bash, and %%timeit_**.