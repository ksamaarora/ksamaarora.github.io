---
layout: default
title: Register an Mlflow model
---

### Model Signatures

**Method 1: Sample code of model signature inferred from dataset**

```python
import pandas as pd
from sklearn import datasets
from sklearn.ensemble import RandomForestClassifier
import mlflow
import mlflow.sklearn
from mlflow.models.signature import infer_signature

iris = datasets.load_iris()
iris_train = pd.DataFrame(iris.data, columns=iris.feature_names)
clf = RandomForestClassifier(max_depth=7, random_state=0)
clf.fit(iris_train, iris.target)

# Infer the signature from the training dataset and model's predictions
signature = infer_signature(iris_train, clf.predict(iris_train))

# Log the scikit-learn model with the custom signature
mlflow.sklearn.log_model(clf, "iris_rf", signature=signature)
```

**Method 2: Sample code of creating signatures manually**

```python
from mlflow.models.signature import ModelSignature
from mlflow.types.schema import Schema, ColSpec

# Define the schema for the input data
input_schema = Schema([
  ColSpec("double", "sepal length (cm)"),
  ColSpec("double", "sepal width (cm)"),
  ColSpec("double", "petal length (cm)"),
  ColSpec("double", "petal width (cm)"),
])

# Define the schema for the output data
output_schema = Schema([ColSpec("long")])

# Create the signature object
signature = ModelSignature(inputs=input_schema, outputs=output_schema)
```