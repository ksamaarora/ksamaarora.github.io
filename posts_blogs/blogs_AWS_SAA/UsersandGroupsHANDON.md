---
layout: default
title: IAM Users and Groups Hands On 
---

## IAM Users and Groups Hands On 

Go to **IAM Console**

> #### **Note:** IAM is a **global service** and thus **region selection** is **not active** in IAM Console

**Create a user**:
  - **Specify user details:** Give a user name and create an IAM user along with setting a console password
[![Screenshot-2024-07-04-at-4-10-56-PM.png](https://i.postimg.cc/kgPD3y4h/Screenshot-2024-07-04-at-4-10-56-PM.png)](https://postimg.cc/xcg9LMLK)
  - **Set permissions:** Add user to a user group (say user group admin with AdministratorAccess as an attached policy)
[![Screenshot-2024-07-04-at-4-11-36-PM.png](https://i.postimg.cc/ydGYfmtj/Screenshot-2024-07-04-at-4-11-36-PM.png)](https://postimg.cc/PpmjJwtv)
[![Screenshot-2024-07-04-at-4-12-20-PM.png](https://i.postimg.cc/Y2mm50R0/Screenshot-2024-07-04-at-4-12-20-PM.png)](https://postimg.cc/23r6vzPN)
  - **Review and create**
  - Retrieve password

> #### **Note:** User 'ksama' now reflecting in the User groups 'admin' with Permission policy 'AdministratorAccess'  attached via the group admin. 

Now you can **login** to the **IAM user** you created