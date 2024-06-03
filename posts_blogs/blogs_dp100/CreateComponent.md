---
layout: default
title: Sample code to create a Compenent
---

### Sample code to create a Compenent

[![Screenshot-2024-06-04-at-1-49-54-AM.png](https://i.postimg.cc/nc8gsyjm/Screenshot-2024-06-04-at-1-49-54-AM.png)](https://postimg.cc/9zpJKNBX)

> ### Step 1: Script named _**prep.py**_ to prepare data

```python
# import libraries
import argparse
import pandas as pd
import numpy as np
from pathlib import Path
from sklearn.preprocessing import MinMaxScaler

# setup arg parser
parser = argparse.ArgumentParser()

# add arguments
parser.add_argument("--input_data", dest='input_data',
                    type=str)
parser.add_argument("--output_data", dest='output_data',
                    type=str)

# parse args
args = parser.parse_args()

# read the data
df = pd.read_csv(args.input_data)

# remove missing values
df = df.dropna()

# normalize the data    
scaler = MinMaxScaler()
num_cols = ['feature1','feature2','feature3','feature4']
df[num_cols] = scaler.fit_transform(df[num_cols])

# save the data as a csv
output_df = df.to_csv(
    (Path(args.output_data) / "prepped-data.csv"), 
    index = False
)
```

> ### Step 2: Create YAML file

To **create component** for _**prep.py**_ **script**, you will **need YAML file** _**prep.yml**_ (stored in src folder)

```yml
$schema: https://azuremlschemas.azureedge.net/latest/commandComponent.schema.json
name: prep_data
display_name: Prepare training data
version: 1
type: command
inputs:
  input_data: 
    type: uri_file
outputs:
  output_data:
    type: uri_file
code: ./src
environment: azureml:AzureML-sklearn-0.24-ubuntu18.04-py37-cpu@latest
command: >-
  python prep.py 
  --input_data ${{inputs.input_data}}
  --output_data ${{outputs.output_data}}
```

> ### Step 3: Load Component

```python
from azure.ai.ml import load_component
parent_dir = ""

loaded_component_prep = load_component(source=parent_dir + "./prep.yml")
```

> ### Step 4: Register Component

[![Screenshot-2024-06-04-at-1-51-55-AM.png](https://i.postimg.cc/V6800L8T/Screenshot-2024-06-04-at-1-51-55-AM.png)](https://postimg.cc/Mc9phwXb)

**When loaded component**, **register** the component.

```python
prep = ml_client.components.create_or_update(prepare_data_component)
```