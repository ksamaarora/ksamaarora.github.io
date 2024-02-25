---
layout: post
title:  "Azure Fundamentals AZ-900"
date:   2024-01-13 09:29:20 +0700
tags:
  - cloud
  - azure
categories: jekyll update
usemathjax: true
---

### Module 1 - Describe Cloud Computing

Cloud computing is the delivery of computing services, including common IT infrastructure such as virtual machines, storage, databases, and networking, over the internet.

#### Shared Responsibility Model

- **Traditional corporate datacenter:**
  - The company is responsible for maintaining the physical space, ensuring security, and maintaining or replacing the servers if anything happens.
  - The IT department is responsible for maintaining all the infrastructure and software needed to keep the datacenter up and running.

- **Shared Responsibility Model (IaaS, SaaS, PaaS):**
  - Cloud Provider manages:
    - Security, power, cooling, and network connectivity.
    - Physical datacenter, physical network, and physical hosts.

  - Consumer manages:
    - Data and information stored in the cloud.
    - Devices connected to the cloud.
    - Accounts and identities of the people, services, and devices within your organization.

- The service model will determine the responsibility of OS, network controls, applications, identity, and infrastructure.

<!-- ![Model pic](models.png) -->

![test](https://cdn.discordapp.com/attachments/1173139022688829511/1179358049308266557/models.png?ex=65e83bc6&is=65d5c6c6&hm=4d76d6ac6fb5e3ee35dadb00c462dd9aa7d1195805e8c8570f38939118e5e101&)

<!-- 
<figure>
<img src="{{ page.image }}" alt="models image">
<figcaption>Fig 1. Models</figcaption>
</figure>
 -->


### **CLOUD MODELS**

- **Private Cloud:**
   - Used by a single entity.
   - The company has control over resources and security.
   - Greater cost and fewer benefits.
   - Hosted from an on-site datacenter.
   - Involves initial capital expenditure (CapEx).
   - Hardware maintenance is required.
   - Deep technical skills are necessary.
   - Best fit to run legacy applications.
   - Customers have the highest degree of control.

- **Public Cloud:**
   - Controlled and maintained by a third-party provider.
   - General public availability.
   - No capital expenditure (CapEx).
   - Organizations pay only for what they use.
   - Organizations don't have complete control over resources and security.
   - No technical skills required.
   - Customers have the lowest degree of control.

- **Hybrid Cloud:**
   - Uses both public and private cloud.
   - Offers more flexibility.
   - Can be used to provide an extra layer of security.
   - Organizations control security, compliance, and legal requirements.
   - More expensive.
   - Deep technical skills are extremely necessary.
   - Managing difficulty.
   - Customers have a moderate degree of control.

- **Multi-Cloud:**
   - Uses two or more (multiple) public cloud providers and manages resources and security in all.

- **Azure Arc:**
   - A set of technologies that help manage your cloud environment, whether it's public, private, hybrid, or multi-cloud.

- **Azure VMware Solution:**
   - A service offered by Microsoft that allows you to take your existing VMware setup and move it into the Azure cloud.
   - Use your own VMware applications and store data in the cloud, whether public or hybrid.

### Consumption-Based Model

There are two types of expenses:

#### **Capital Expenditure (CapEx):**
   - One-time, up-front expenditure.

#### **Operational Expenditure (OpEx):**
   - Spending money on services or products.
   - Cloud Computing follows a consumption-based model (pay as you go).
   - There is no upfront cost, and there's no need to purchase and manage costly infrastructure that users might not use to the fullest.
   - You have the ability to pay for more resources when used and stop paying when not used.

### Conclusion

Cloud computing is a way to rent compute power and storage from someone else's data center. You are billed for only what you use, and the cloud provider manages the underlying infrastructure for you, enabling you to quickly solve the toughest challenges and bring cutting-edge solutions to your users.