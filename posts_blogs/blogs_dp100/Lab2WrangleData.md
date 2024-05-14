---
layout: default
title: Lab 2 Create ML Workspace in Azure
---

### Wrangle Data with Python in Azure ML - Lab 2

> Step 1: Select workspace and launch **Azure ML Studio**

> Step 2: Go to **notebooks** and create a notebook and you can see a **pre-deployed compute** running. 
    When prompted, authenticate to the compute. 

> Step 3: **Load a Dataframe**

```python
import pandas as pd
my_dataframe = pd.read_csv("https://raw.githubusercontent.com/pluralsight-cloud/DP-100-Designing-and-Implementing-a-Data-Science-Solution-on-Azure/main/MedicalClaimSummary.csv")
my_dataframe.head(1000)
```

[![Screenshot-2024-05-15-at-12-38-43-AM.png](https://i.postimg.cc/Rhcp8gYv/Screenshot-2024-05-15-at-12-38-43-AM.png)](https://postimg.cc/T53c5JGs)

> Step 4: Wrangle - **Replace Missing Strings** (replace **NaN** values)

```python
my_dataframe.fillna(value={"Payment Status": "Unkown"}, inplace=True)
my_dataframe.fillna(value={"Claim Network Status": "Unkown"}, inplace=True)
my_dataframe.head(1000)
```

> Step 5: Wrangle - **Delete Rows with any empty columns**

```python
my_dataframe.dropna(inplace=True)
my_dataframe.head(1000)
```

> Step 6: Wrangle - **Remove Duplicate Rows**

```python
my_dataframe.drop_duplicates(inplace=True)
my_dataframe.sort_index(inplace=True)
my_dataframe.head(1000)
```

> Step 7: **Save the transformed data** (Refresh the file tree and you will see the new csv file)

[![Screenshot-2024-05-15-at-12-45-15-AM.png](https://i.postimg.cc/Hstd8zLG/Screenshot-2024-05-15-at-12-45-15-AM.png)](https://postimg.cc/MvXhhyRt)

```python
my_dataframe.to_csv("WrangledData.csv")
```

[![Screenshot-2024-05-15-at-12-45-53-AM.png](https://i.postimg.cc/rp0BjNqw/Screenshot-2024-05-15-at-12-45-53-AM.png)](https://postimg.cc/v1y2H91J)


