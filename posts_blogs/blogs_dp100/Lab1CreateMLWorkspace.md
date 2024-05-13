---
layout: default
title: Lab 1 Create ML Workspace in Azure
---

### Create Machine Learning Workspace in Azure - Lab 1

- Everything in Azure goes into a resource group
- Create **Azure ML Workspace:** Save configuration/template of workspace if needed for future use.
- **Application Insights**, **Key Vaults**, and **Storage account** created: Ensure these are set up for your workspace.
- Go to Azure ML **Studio**
- Create Compute Instance **(VM) for notebook** to run
- **Stop VM**

### **DETAILED STEPS:**
> #### Step 1:
- Got to Azure Machine Learning and create a new ML Workspace 
- Save configuration/template of workspace using Azure Resource Manager (ARM) by clicking on download button if needed for future use
[![Screenshot-2024-05-13-at-2-53-34-PM.png](https://i.postimg.cc/VNmJgbbc/Screenshot-2024-05-13-at-2-53-34-PM.png)](https://postimg.cc/mPpZ2kwd)

> #### Step 2:
- Once deployment is complete, go to our resource and check the Key Vault and Application Insight that has been created. Now go to Azure ML Studio
[![temp-Imagelsf-Ejv.avif](https://i.postimg.cc/dVq7myCc/temp-Imagelsf-Ejv.avif)](https://postimg.cc/gnTkGr4g)

> #### Step 3:
- Now in the ML Studio, create some compute VM
- To power a notebook we will create a compute instance.
[![Screenshot-2024-05-13-at-2-55-57-PM.png](https://i.postimg.cc/T1w7DwcV/Screenshot-2024-05-13-at-2-55-57-PM.png)](https://postimg.cc/Kk6DXmwj)


> #### Step 4:
- To test the compute we will create a jupyter notebook
[![Screenshot-2024-05-13-at-2-57-16-PM.png](https://i.postimg.cc/MG67NPrs/Screenshot-2024-05-13-at-2-57-16-PM.png)](https://postimg.cc/gx7L6DpR)

> #### Step 5:
- Test a program. We will use Azure ML Kernel as it has all the tools installed
[![Screenshot-2024-05-13-at-2-58-04-PM.png](https://i.postimg.cc/0yB51rVL/Screenshot-2024-05-13-at-2-58-04-PM.png)](https://postimg.cc/sM5Cpfdc)

> #### Step 6:
- Remember to stop the virtual machine after use to avoid unnecessary charges.
[![Screenshot-2024-05-13-at-2-58-32-PM.png](https://i.postimg.cc/d1mK309Q/Screenshot-2024-05-13-at-2-58-32-PM.png)](https://postimg.cc/ZBRQD4gX)


