---
layout: default
title: Lab 4 Using Azure Automated Machine Learning
---

### Using Azure Automated Machine Learning - Lab 4

[![Screenshot-2024-05-16-at-5-54-46-PM.png](https://i.postimg.cc/YqB1dHTn/Screenshot-2024-05-16-at-5-54-46-PM.png)](https://postimg.cc/5jpYtZ4L)

> Open Azure ML Studio -> Click Automated ML

> **Step 1:** **Create a New Automated ML Job**

- **Select Task Type**:  **Five categories of algorithm available in Azure Automated ML**
  - **Regression** predict numerical values. 
  - **Classification** predict numerical values.
  - **Time-series** predict future numerical values based on time-series data e.g. predicting future sales.
  - **Natural Language Processing** extract insights from text
  - **Computer Vision** classify images or detect objects in images 

[![Screenshot-2024-05-16-at-4-08-02-AM.png](https://i.postimg.cc/SN5V28qC/Screenshot-2024-05-16-at-4-08-02-AM.png)](https://postimg.cc/fJcY1VVR)

- **Create a Data Asset**: 
  - Data type:
    - **Name**: Enter a name for your data asset.
    - **Select Type**:  **Tabular**/Table(mltable)

[![Screenshot-2024-05-16-at-4-10-42-AM.png](https://i.postimg.cc/L5wMqXND/Screenshot-2024-05-16-at-4-10-42-AM.png)](https://postimg.cc/XBfPmVMB)

  - **Data source**: Azure Storage/Local files/SQL databases/**Web files**/Azure Open Datasets

  [![Screenshot-2024-05-16-at-4-12-13-AM.png](https://i.postimg.cc/QM0w9CM7/Screenshot-2024-05-16-at-4-12-13-AM.png)](https://postimg.cc/PLv20tYf)

  - Enter **web url** 

  [![Screenshot-2024-05-16-at-4-12-34-AM.png](https://i.postimg.cc/j2JFFh46/Screenshot-2024-05-16-at-4-12-34-AM.png)](https://postimg.cc/5QbgHLGj)

  - Settings -> Schema -> Review+Create

  [![Screenshot-2024-05-16-at-4-12-58-AM.png](https://i.postimg.cc/FzgBvHw1/Screenshot-2024-05-16-at-4-12-58-AM.png)](https://postimg.cc/n9rkYpFt)

- **Select  the Dataset and click next**
- **Task Settings Configuration**
  - **Select Target Column**: Choose the column you want to predict (your target variable).
  - **Set Experiment Timeout**: Set the timeout for the experiment to 15 minutes.
  - **Enable Early Termination**: Check the "Enable early termination" checkbox to stop the experiment early if it is not performing well.
- **Select Compute Type**: **Compute cluster**/Compute Instance/Serverless

> #### IMP Note:
To apply **one-hot encoding** (**encoding transformation**) to categorical features in a dataset while using automated ML, **enable featurization**. **Impute missing values** is a technique that will be **tried when activating featurization** but cannot be enabled on its own. **Feature scaling** and **normalisation** is **enabled by default**. 

[![Screenshot-2024-05-16-at-4-15-14-AM.png](https://i.postimg.cc/GthkB3H4/Screenshot-2024-05-16-at-4-15-14-AM.png)](https://postimg.cc/dkp7pYRF)

- **Submit the Job**: Click "Submit". The job will run for approximately 30 minutes.

- **Note:*** **Job Status** can be following:
  - **Queued:** The job is waiting for compute to become available.
  - **Preparing:** The compute cluster is resizing or the environment is being installed on the compute target.
  - **Running:** The training script is being executed.
  - **Finalizing:** The training script ran and the job is being updated with all final information.
  - **Completed**: The job successfully completed and is terminated.  
  - **Failed:** The job failed and is terminated.


> **Step 2: Evaluate & Compare Model***

- **View Models + Child Jobs**: Once the job is complete, navigate to the "Models + Child jobs" section.
- **Best Algorithm**: You should see that the best algorithm selected by Azure is "Voting Ensemble".
- **Data guardrails:** This tab shows whether training data has any issue

[![Screenshot-2024-05-16-at-4-15-57-AM.png](https://i.postimg.cc/QtS7rL0h/Screenshot-2024-05-16-at-4-15-57-AM.png)](https://postimg.cc/dkk38xbx)

- **Normalized Root Mean Squared Error**: Lower the value, the better the model

[![Screenshot-2024-05-16-at-4-16-49-AM.png](https://i.postimg.cc/FRfYwfdg/Screenshot-2024-05-16-at-4-16-49-AM.png)](https://postimg.cc/zbrDgGkV)

> **Step 3: Deploy the Model**

- **Deploy**: Real-time endpoint/Batch endpoint/**Web service**

[![Screenshot-2024-05-16-at-4-20-19-AM.png](https://i.postimg.cc/cLqBhSzb/Screenshot-2024-05-16-at-4-20-19-AM.png)](https://postimg.cc/KRNTcdxP)

- **Real-Time Predictions**
Real-time predictions provide **instant recommendations** based on customer actions, requiring **continuous compute resources**. Azure Container Instances **(ACI)** or Azure Kubernetes Service **(AKS)** are ideal for this, offering lightweight and cost-effective infrastructure solutions that ensure your model is **always available**.

- **Batch Predictions**
Batch predictions are **scheduled and less frequent**, such as weekly sales forecasts. This approach utilizes **compute clusters** to process data in parallel, making it efficient for **handling large datasets** periodically.

[![Screenshot-2024-05-22-at-3-10-12-PM.png](https://i.postimg.cc/J4D893nY/Screenshot-2024-05-22-at-3-10-12-PM.png)](https://postimg.cc/tYj86xFF)

   - Click "Deploy".
   - **Name**: Enter a name for the deployment.
   - **Compute Type**:  AksCompute/**Azure Container Instance**
   - **Advanced Settings**:
     - **CPU Reserve Capacity**: Set to 1.
     - **Memory Reserve Capacity**: Set to 1.
   - Click "Deploy".

> **Step 4: Test the Deployed Model**

- **Find Deployment Endpoint**: After deployment, the endpoint can be found under "Endpoints".

[![Screenshot-2024-05-16-at-4-21-07-AM.png](https://i.postimg.cc/SKR7df4g/Screenshot-2024-05-16-at-4-21-07-AM.png)](https://postimg.cc/2qpZ8vVW)

- **Test Tab**: Select the endpoint and navigate to the "Test" tab.
- **Enter Test Data**: Enter values to test the model's predictions.
- **Check Prediction**: For the given data, check how close the predicted value is to 17.5.

[![Screenshot-2024-05-16-at-4-21-53-AM.png](https://i.postimg.cc/fb1XK4Bb/Screenshot-2024-05-16-at-4-21-53-AM.png)](https://postimg.cc/4Kbmf0CC)


> **Step 5: Evaluate Model**

[![Screenshot-2024-05-16-at-6-02-44-PM.png](https://i.postimg.cc/kgvQzpWQ/Screenshot-2024-05-16-at-6-02-44-PM.png)](https://postimg.cc/zy3HRptv)

> #### IMP NOTE:
- **Regression Metrics:** Mean Absolute Error (**MAE**), Root Mean Squared Error (**RMSE**), Relative Squared Error (**RSE**), Relative Absolute Error (**RAE**) and R Square/Coefficient of Determination (**R^2**).
- **Classification Metrics:** **Accuracy**, **Precision**, **Recall**, **F1 Score**, **AUC**.

[![Screenshot-2024-06-06-at-3-16-34-PM.png](https://i.postimg.cc/T35kB2gP/Screenshot-2024-06-06-at-3-16-34-PM.png)](https://postimg.cc/G4rJyCM0)

> **IMP NOTE**
- **Precision metric** will result in a model that **minimises FPR** (false positive rate)
- **Recall metric** will result in a model that **minimises FNR** (false negative rate)
- **Accuracy metric** will result in a model with **highest accuracy**
- **AUC metric** will result in a model with **highest area under receiver operating** characteristic curve

- To **explore a model**, can **generate explanations** for each model that has been trained. Can **specify explanations** for best performing mode. If however, you're **interested in the interpretability of another model**, can select the **model in overview** and **select Explain model**.



