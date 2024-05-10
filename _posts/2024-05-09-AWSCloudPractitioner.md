---
layout: post
title:  "AWS Cloud Practitioner"
date:   2024-05-08 09:29:20 +0700
tags:
  - cloud
categories: jekyll update
usemathjax: true
---

> ### OVERVIEW OF AWS

Cloud is a collection of services hosted on servers in different regions.

**Regions and Availability Zones:**

- **Region** is a **physical location** somewhere in the world, where they put their **data centers**, which have the servers that **host** all of their **services**.
Currently AWS  has regions in **North & South America**, **Europe**, **Middle East**, **Africa** and the **Asia Pacific**

- **Availability Zones**: Inside a region we have Azs. **Each region** has **multiple isolated and physically separated AZ in a geographic area**. They all have **independent power, cooling and physical security** and they all are connected to each other via ultra high speed and low latency networks

[![Screenshot-2024-05-10-at-12-04-58-PM.png](https://i.postimg.cc/kGcVY9Fb/Screenshot-2024-05-10-at-12-04-58-PM.png)](https://postimg.cc/MfnKXCL6)

> ### SECURITY AND IDENTITY

> #### Services for Data protection:
  - **Amazon Macie:** to discover and protect sensitive data
  - **AWS Key Management Service:** to store and manage encryption keys
  - **AWS CloudHSM:** for hardware based key storage
  - **AWS Certificate Manager:** to provision, manage and deploy SSL and TLS security certificates
  - **AWS Secrets Manager:** to rotate, manage and retrieve secrets - passwords, keys or tokens 

**AWS Secrets Manager:**
  - It is service that protects your secrets that are needed to access your applications, services and resources.
  - In AWS, you can change password by sending request to secrets manager. Thus the password is fetched by the secrets manager and sent to the service that requires it. Thus remebering of passowrd is no longer required.
  - Secrets manager can also change your password at regular intervals and update it both in where they are stored and on the service where it is being used.

> #### Services for Infrastructure Protection:
  - **AWS Shield:** for denial of service protection is 
  - **AWS Web Application Firewall (AWS WAF):** to filter malicious website traffic
  - **AWS Firewall Manager:** to centrally manage firewall rule

> #### Service for Threat Detection:
  - **Amazon GuardDuty:** to automatically detect threats
  - **Amazon Inspector:** to analyze application security
  - **AWS Config:** to record and evaluate configurations of your AWS resources
  - **AWS CloudTrail:** to track use activity and API usage

> #### Service for Identity Management:
  - **AWS Identity and Access Management (AWS IAM):** to securely manage access to your AWS account
  - **AWS Single sign-on:** to implement cloud single sign-on
  - **Amazon Cognito:** to manage identity inside applications
  - **AWS Directory Service:** to implement and manage Microsoft Active Directory 
  - **AWS Organizations:** to centrally govern and manage multiple AWS accounts in one place  

**AWS Identity Access Management:** 

  - IAM is a way to **manage who can access** what in your **AWS accounts**. You **can create users and groups** and **set permissions** on both of them to whether allow or deny access to AWS resources via policies. **IAM is free** and is included in every AWS Account. IAM is a **global service on AWS**.

  - Two **main features of IAM:**

    - **IAM Users:** 
      - Once you **create an AWS Account**, you are given a **root user** login. This is the main account you login to your AWS resources with. You are then **able to create an IAM user**, which is another name for a username and password that can login to your AWS account, but you get to **decide what they have access** to. 
      - **Users** can also be **merged into groups**, making it easier. **Policies** can also be applied to groups so you don’t have to give access to all of your developers individually. 
      - Policies are usually created in the **IAM console**, which has both a visual editor and a JSON editor.
      - For **e.g.** - You are owner of company and you have a team of 10 developers, 5 sales, 2 testers and a release engineer. And you have a bunch of services that they have to be given access to. Depending on the requirment these are given specific access as shown. 
     
    - **IAM Roles:** 
      - **Roles allow you to delegate access to a user or a service**. Not only can a user assume a role but a service can also assume a role. 
      - **E.g.** you may be running a VM which hosts your website, and as part of your website you have a database running in an AWS database service. You can **create a role** which **allows someone to access your database service** and then u **can tell VM** to **use that role** and when they use that role it **grants them, only them, permission** to access you database. 
  
**AWS Directory Service:**
  - **Directory** is a database of people which contains all the login information for all the users on the network. When you try to access, your credentials are checked against this directory if you have access or not.
  - **AWS Directory service is a managed service offering which provides the directories for you without having to run the servers yourself.**
  - AWS offers **Managed Microsoft Active Directory** and **Managed Simple Active Directory**. 
  - If **any service fails**, the service **automatically replaces the failed server** with a working one.

> ### COMPUTE

Compute refers to using a computer to process something.

> #### Instances:
  - **Amazon Elastic Compute Cloud (EC2):** Service that provides secure and resizable virtual machines in the cloud - allows to rent virtual computers called EC2 Instances - different EC2 types can be CPU, memory, storage and speed - on demand pricing options 
  - **EC2 Spot:** Service which helps you run fault tolerance workloads for up to 90% of the normal price
  - **Amazon EC2 Auto Scaling:** Service which can automatically add or remove computing capacity based on demand
  - **Amazon Lightsail:** Service which provides a really easy to use cloud platform to build an application or website    

> #### Containers:
Containers are like portable, self-contained packages for software that contains all necessary code, libraries and settings so that program can run smoothly.
  - **Amazon Elastic Container Service (Amazon ECS):** Service to run secure, reliable and scalable containers
  - **Amazon Elastic Container Registry (Amazon ECR):** Service to store manage and deploy container images
  - **Amazon Elastic Kubernetes Service (Amazon EKS):** A fully managed Kubernetes service

> #### Serverless:
- **AWS Lambda:** A compute service which allows you to run code without servers 
  
> #### Edge:
  - **AWS Outposts:** Service which lets you run your AWS services on your own servers instead of Amazons
  - **AWS Snow Family:** Service that lets you bring lot of data into AWS is called 
  - **AWS Wavelength:** Service that lets you access AWS services from 5g devices without having to go via the internet
  - **VMware Cloud:** Service which helps in migrating the VMWare workloads to AWS
  - **AWS Local Zones:** Service which lets you run latency sensitive applications closer to end users
  
