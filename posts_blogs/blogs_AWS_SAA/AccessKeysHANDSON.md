---
layout: default
title: AWS Access Keys, CLI and SDK Hands On
---

## AWS Access Keys, CLI and SDK Hands On

> To check AWS version : **_aws --version_**

> **Create a Access Key:** 
- Select a user  -> go to **Security Credentials** -> Create Access Key

[![Screenshot-2024-07-06-at-9-08-40-PM.png](https://i.postimg.cc/B6Ydf7Sb/Screenshot-2024-07-06-at-9-08-40-PM.png)](https://postimg.cc/wyNWhVsY)

**Note:** AWS recommends **alternatives** to each use case. Below are alternatives given for CLI
[![Screenshot-2024-07-06-at-9-09-19-PM.png](https://i.postimg.cc/3x35pvcK/Screenshot-2024-07-06-at-9-09-19-PM.png)](https://postimg.cc/ZCsMzCmg)

> After creating Access Key, **open terminal** and **configure** aws using **_aws configure_** and then **list** users of iam using **_aws iam list-users_**
[![Screenshot-2024-07-06-at-9-33-56-PM.png](https://i.postimg.cc/Xvn0dDQ1/Screenshot-2024-07-06-at-9-33-56-PM.png)](https://postimg.cc/ZWsghjk6)

**Note:** the command aws iam list-users will **only give output** if **user** is **assigned** a **permission policy** or else it will give an **error (Access Denied)** when calling ListUsers operation.
[![Screenshot-2024-07-06-at-9-34-37-PM.png](https://i.postimg.cc/XJG3YB2n/Screenshot-2024-07-06-at-9-34-37-PM.png)](https://postimg.cc/bDh46rc5)

> The **AWS CLI** gives **similar** info as the **AWS Management Console** 

### Alternative to using terminal is CloudShell

[![Screenshot-2024-07-06-at-11-16-48-PM.png](https://i.postimg.cc/43tgjL5s/Screenshot-2024-07-06-at-11-16-48-PM.png)](https://postimg.cc/Y4pZWxZs)

[![Screenshot-2024-07-06-at-11-17-16-PM.png](https://i.postimg.cc/kGMP6ndg/Screenshot-2024-07-06-at-11-17-16-PM.png)](https://postimg.cc/HcNhF1xq)