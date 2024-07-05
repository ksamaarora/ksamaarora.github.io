---
layout: default
title: IAM Policy Hands On 
---

## IAM Policy Hands On

- If you **remove a user** from a **group**, the **inherited policy** permissions will be **lost** by the user. 
[![Screenshot-2024-07-04-at-10-49-37-PM.png](https://i.postimg.cc/Y95ryz0t/Screenshot-2024-07-04-at-10-49-37-PM.png)](https://postimg.cc/LYVFJfjW)

- If say through the root user, you attach a policy say **IAMReadOnlyAccess** to the user, you will only be **able to read anything** on the IAM. You will be **denied** of **any other access** if tried. 
[![Screenshot-2024-07-04-at-10-52-20-PM.png](https://i.postimg.cc/HkRhMZhW/Screenshot-2024-07-04-at-10-52-20-PM.png)](https://postimg.cc/K17fSNbC)

- **Example:** you create a **user group** names developer and attach a policy **AlexaForBusiness** to it, and a user group **admin** with policy **AdministratorAccess**. If you **add a user** say ksama to both these groups, and also **attach** a policy say **IAMReadOnlyAccess directly** to this user, then this user will have 3 permission policies attached. 
[![Screenshot-2024-07-04-at-11-00-33-PM.png](https://i.postimg.cc/8cw68Y6h/Screenshot-2024-07-04-at-11-00-33-PM.png)](https://postimg.cc/K3kzBJQz)

> #### Looking at some policies in detail:

- **_AdministratorAccess Policy_**: All services have full access to this policy. **Allows any action (*) on any resource (*)**. 
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "*",
            "Resource": "*"
        }
    ]
}
```

- **_IAMReadOnlyAccess_**: IAM is authorised with **_Full: List Limited: Read_**. **Note:** **_Get*_** means that **anything** that **starts** with **Get** and has **something afterwards** is **authorized**.
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iam:GenerateCredentialReport",
                "iam:GenerateServiceLastAccessedDetails",
                "iam:Get*",
                "iam:List*",
                "iam:SimulateCustomPolicy",
                "iam:SimulatePrincipalPolicy"
            ],
            "Resource": "*"
        }
    ]
}
```

> ### Create Policy using Visual Editor or a JSON Editor

- Using **Visual Editor**, say u add two actions **_ListUser_** and **_GetUser_**, and create a new policy names MyIAMPermissions
[![Screenshot-2024-07-04-at-11-37-20-PM.png](https://i.postimg.cc/3xS63CBs/Screenshot-2024-07-04-at-11-37-20-PM.png)](https://postimg.cc/k2SwcSLs)

- Using **JSON editor**, u just need to fill actions and resource using dropdown
[![Screenshot-2024-07-04-at-11-38-37-PM.png](https://i.postimg.cc/h4NVRJT2/Screenshot-2024-07-04-at-11-38-37-PM.png)](https://postimg.cc/F1gYjHPS)