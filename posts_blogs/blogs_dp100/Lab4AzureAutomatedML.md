---
layout: default
title: Lab 4 Using Azure Automated Machine Learning
---

### Using Azure Automated Machine Learning - Lab 4

> Open Azure ML Studio -> Click Automated ML

> **Step 1:** **Create a New Automated ML Job**

- **Select Task Type**:  Classification/**Regression**/Time Series Forecasting/NLP/Computer Vision
[![Screenshot-2024-05-16-at-4-08-02-AM.png](https://i.postimg.cc/SN5V28qC/Screenshot-2024-05-16-at-4-08-02-AM.png)](https://postimg.cc/fJcY1VVR)
- **Create a Data Asset**: 
  - Data type:
    - **Name**: Enter a name for your data asset.
    - **Select Type**:  **Tabular**/Table(mltable)
[![Screenshot-2024-05-16-at-4-10-42-AM.png](https://i.postimg.cc/L5wMqXND/Screenshot-2024-05-16-at-4-10-42-AM.png)](https://postimg.cc/XBfPmVMB)
  - Data source: Azure Storage/Local files/SQL databases/**Web files**/Azure Open Datasets
  [![Screenshot-2024-05-16-at-4-12-13-AM.png](https://i.postimg.cc/QM0w9CM7/Screenshot-2024-05-16-at-4-12-13-AM.png)](https://postimg.cc/PLv20tYf)
  - Enter web url 
  [![Screenshot-2024-05-16-at-4-12-34-AM.png](https://i.postimg.cc/j2JFFh46/Screenshot-2024-05-16-at-4-12-34-AM.png)](https://postimg.cc/5QbgHLGj)
  - Settings -> Schema -> Review+Create
  [![Screenshot-2024-05-16-at-4-12-58-AM.png](https://i.postimg.cc/FzgBvHw1/Screenshot-2024-05-16-at-4-12-58-AM.png)](https://postimg.cc/n9rkYpFt)
- **Select  the Dataset and click next**
- **Task Settings Configuration**
  - **Select Target Column**: Choose the column you want to predict (your target variable).
  - **Set Experiment Timeout**: Set the timeout for the experiment to 15 minutes.
  - **Enable Early Termination**: Check the "Enable early termination" checkbox to stop the experiment early if it is not performing well.
- **Select Compute Type**: **Compute cluster**/Compute Instance/Serverless
[![Screenshot-2024-05-16-at-4-15-14-AM.png](https://i.postimg.cc/GthkB3H4/Screenshot-2024-05-16-at-4-15-14-AM.png)](https://postimg.cc/dkp7pYRF)
- **Submit the Job**: Click "Submit". The job will run for approximately 30 minutes.

> **Step 2: Evaluate the Model**

- **View Models + Child Jobs**: Once the job is complete, navigate to the "Models + Child jobs" section.
- **Best Algorithm**: You should see that the best algorithm selected by Azure is "Voting Ensemble".
[![Screenshot-2024-05-16-at-4-15-57-AM.png](https://i.postimg.cc/QtS7rL0h/Screenshot-2024-05-16-at-4-15-57-AM.png)](https://postimg.cc/dkk38xbx)
- **Normalized Root Mean Squared Error**: Lower the value, the better the model
[![Screenshot-2024-05-16-at-4-16-49-AM.png](https://i.postimg.cc/FRfYwfdg/Screenshot-2024-05-16-at-4-16-49-AM.png)](https://postimg.cc/zbrDgGkV)

> **Step 3: Deploy the Model**

- **Deploy**: Real-time endpoint/Batch endpoint/**Web service**
[![Screenshot-2024-05-16-at-4-20-19-AM.png](https://i.postimg.cc/cLqBhSzb/Screenshot-2024-05-16-at-4-20-19-AM.png)](https://postimg.cc/KRNTcdxP)
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

