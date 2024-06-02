---
layout: default
title: Data Wrangling
---

- Step 1: Open a notebook with a running ML Azure Kernel

- Step 2: Create **ML Client** and a **datastore** (code mentioned before)

- Step 3: Build a **URI** OR **Directly grab** it in the **Studio UI**

```python
# Azure Machine Learning workspace details:
subscription = '<subscription_id>'
resource_group = '<resource_group>'
workspace = '<workspace>'
datastore_name = '<datastore>'
path_on_datastore = '<path>'

# Long-form Datastore URI format:
uri = f'azureml://subscriptions/{subscription}/resourcegroups/{resource_group}/workspaces/{workspace}/datastores/{datastore_name}/paths/{path_on_datastore}'
```

OR go to Data -> specific Datastore -> select csv file -> copy URI (Datastore URI or Storage URI)
  - **Note:** The **Datastore URI** is only **applicable to Azure ML** and the **Storage URI** is a more generic storage endpoint, which is used only **outside Azure ML**.

- Step 4: Load a **Pandas Dataframe**

```python
# Import pandas library
import pandas as pd

# Populate dataframe "my_dataframe" using the pandas read CSV method by passing in the URI acquired
my_dataframe = pd.read_csv("URI")

# Then run dataframe head passing in a value for the number of rows you want to return
my_dataframe.head(1000)
```

- Step 5: **Wrangle** - Replace **Missing** Strings

```python
# Fill missing values in the "Claim Network Status" column with "Unkown" and update the dataframe in place
my_dataframe.fillna(
    value={"Claim Network Status": "Unkown"}, inplace=True)

# Fill missing values in the "Payment Status" column with "Unkown" and update the dataframe in place
my_dataframe.fillna(
    value={"Payment Status": "Unkown"}, inplace=True)

# Return the first 1000 rows of the dataframe
my_dataframe.head(1000)
```

- Step 6: **Wrangle** - **Delete Rows** With any **Empty** Columns

```python
# Drop rows with any missing values and update the dataframe in place
my_dataframe.dropna(inplace=True)

# Return the first 1000 rows of the dataframe
my_dataframe.head(1000)
```

> ### Wrangling Data with Apache Spark

- Step 1: Create a **compute** to power the notebook - Compute instance / Synapse Spark Pool / Azure ML Serverless Spark

- Step 2: Open a **notebook** and we use **Azure ML Serverless Spark** as compute for ease of use

- Step 3: Build a **URI** or grab it from the Studio UI

- Step 4: Load a **PySpark Pandas Dataframe**

```python
# Import pyspark pandas library
import pyspark.pandas as pd
my_dataframe = pd.read_csv("URI")
my_dataframe.head(1000)
```

- Step 5: Wrangle - Replace **Missing** Strings (code given above)

- Step 6: Wrangle - **Delete rows** with any **empty** columns (code given above)

- Step 7: **Wrangle** - Remove **Duplicate** Rows 

```python
# Drop duplicate rows and update the dataframe in place
my_dataframe.drop_duplicates(inplace=True)

# Sort the dataframe by its index and update the dataframe in place
my_dataframe.sort_index(inplace=True)

# Return the first 1000 rows of the dataframe
my_dataframe.head(1000)
```

- Step 8: **Save** the Transformed Data

```python
# Save the dataframe to a CSV file at the specified Azure Data Lake Storage path
my_dataframe.to_csv(
    "abfss://<FILE_SYSTEM_NAME>@<STORAGE_ACCOUNT_NAME>.dfs.core.windows.net/data/wrangled"
    )
```