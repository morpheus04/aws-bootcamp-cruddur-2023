# Week 0 — Billing and Architecture

#### Table of Contents

+ [Required Homework](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/main/journal/week0.md#required-homework-instructional-homework)
  - [Lucid Diagrams](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/main/journal/week0.md#lucid-diagrams)
  - [Budgets & Billing Alarm](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/main/journal/week0.md#budgets--billing-alarm)
      - [Create a Budget](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/main/journal/week0.md#create-a-budget)
      - [Create a Billing Alarm](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/main/journal/week0.md#create-a-billing-alarm)
+ [Homework Challenges](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/main/journal/week0.md#homework-challenges)
  - [Budgets & Billing Alarm](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/main/journal/week0.md#budgets--billing-alarm-1)
      - [Create a Budget](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/main/journal/week0.md#create-a-budget-1)
  - [Destroy root account credentials](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/main/journal/week0.md#budgets--billing-alarm-1)
  - [Set MFA](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/main/journal/week0.md#budgets--billing-alarm-1)
  - [IAM role](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/main/journal/week0.md#budgets--billing-alarm-1)
  - [EventBridge (Health Dashboard) & SNS Setup](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/main/journal/week0.md#budgets--billing-alarm-1)
  - [Open a support ticket and request a service limit](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/main/journal/week0.md#budgets--billing-alarm-1)

## Required Homework (Instructional Homework)

### Lucid Diagrams
|Task|URL|Screenshots (Images)|
|----|-----|-------|
|Recreate Conceptual Diagram in Lucid Charts or on a Napkin|[Conceptual Diagram](https://lucid.app/lucidchart/621ecb99-b13c-41be-9775-85153ace2582/edit?viewport_loc=-399%2C65%2C2219%2C1089%2C0_0&invitationId=inv_6eecf645-1a68-4568-a410-ccb1bb77fb4e)|![image](https://user-images.githubusercontent.com/37842433/219356770-c133397c-7660-41f1-9ccf-d3ebb7b1f256.png)|
|Recreate Logical Architectual Diagram in Lucid Charts|[Logical Architectual Diagram](https://lucid.app/lucidchart/621ecb99-b13c-41be-9775-85153ace2582/edit?viewport_loc=-148%2C159%2C2219%2C1089%2CxmCwnDjlFT5Z&invitationId=inv_6eecf645-1a68-4568-a410-ccb1bb77fb4e)|![image](https://user-images.githubusercontent.com/37842433/219059219-a714e261-9435-4268-8743-3fe21ed4e40a.png)|  


 ---
 


### Budgets & Billing Alarm

#### <ins>Create a Budget</ins>

The task was to budget for all resources and credits spend. So I created 2 budgets (Cloud-BootCamp-Budget & Track-Credits-Budgets). The *Cloud-BootCamp-Budget* was created via the AWS CLI (using gitpod), whilst the *Track-Credits-Budgets* was created using the AWS Billing portal.

- *Cloud-BootCamp-Budget*

The main budget (set to $100) for the account was created to include all AWS resource monthly spend and threshold alerts created dependent on the % of actual spend vs set amount. This can be seen in the diagrams below

![image](https://user-images.githubusercontent.com/37842433/219105210-78e592f5-fd9d-4e41-950d-45bac18c05ed.png)

An extract of the code as referenced in my repo

[main/aws/json/budget.json](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/main/aws/json/budget.json)

***


- *Track-Credits-Budgets*

The Credits budget was created to use just the "Credits" parameter. The budget was also set @ $5 as seen in the diagram below

![image](https://user-images.githubusercontent.com/37842433/219103833-e913eec7-f53a-4774-a17d-7e57c9a74227.png)

***

#### <ins>Create a Billing Alarm</ins>

The task was to create daily billing alarm for all resource daily spend. The budget was set to a daily amount of $1. The *DailyEstimatedCharges* billing alarm was created via the AWS CLI (using gitpod) and resulted in a CloudWatch been created in AWS.

As part of this process, AWS SNS was setup with an email (this was verified and confirmed as part of the setup). The alarm will send alerts (by subscription to a topic *billing-alarm*) using AWS SNS (Simple Notification Service) to an email address whenver the value is exceeded.

This can be seen in the diagram below

![image](https://user-images.githubusercontent.com/37842433/219127470-d332fb6b-4eeb-4473-9575-4217d1b36cce.png)

An extract of the code showing the creation of the billing alarm as referenced in my repo

[main/aws/json/alarm_config.json](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/main/aws/json/alarm_config.json)

***

## Homework Challenges

### Budgets & Billing Alarm

#### <ins>Create a Budget</ins>

- *Cloud-BootCamp-Budget*

I created threshold alerts created dependent on the % of actual spend vs set amount. This can be seen in the diagrams below

![image](https://user-images.githubusercontent.com/37842433/219121541-70c05e71-f95f-45c5-8740-ea0bb65c6858.png)

An extract of the code showing the creation of 4 threshold alerts (20% - 80%) as referenced in my repo

[main/aws/json/budget-notifications-with-subscribers.json](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/main/aws/json/budget-notifications-with-subscribers.json)

---

### Destroy root account credentials

- Setting up my root credentials keys

The AWS recommendation was not to set this up as seen below

![image](https://user-images.githubusercontent.com/37842433/219369618-98c260cf-c015-476d-a22e-e6b5722f1c0b.png)

However for the purpose of this task, I proceed to set it up

![image](https://user-images.githubusercontent.com/37842433/219370099-065014e3-f820-4970-85dd-48ed9a69f438.png)


- Destroy Keys (Credentials)

I proceeded to destroy the keys. To destroy the keys, it needed to be deactivated first (made inactive)

![image](https://user-images.githubusercontent.com/37842433/219369995-370906ce-5100-45a3-9c18-d99d7df08488.png)
![image](https://user-images.githubusercontent.com/37842433/219372222-70187982-0d0d-4175-936e-1072281a0a4a.png)


Once deactivated, the keys were then deleted

![image](https://user-images.githubusercontent.com/37842433/219372265-e009175c-385c-4928-8fb7-368ce97bcb4a.png)

---

### Set MFA

AWS Multi-Factor Authentication (MFA) is a simple best practice that adds an extra layer of protection on top of user name and password.

![image](https://user-images.githubusercontent.com/37842433/219368967-9be9f6f7-088a-4da5-bd9f-f2fd30c3a69a.png)

![image](https://user-images.githubusercontent.com/37842433/219369039-e7aa93ea-6ae0-4846-a1c1-2c9fa048da9d.png)

---

### IAM role

- Created and IAM Role with policies (permissions attached)

![image](https://user-images.githubusercontent.com/37842433/219373605-3b5c0376-bb7d-460e-9b7f-9807a1091bed.png)

Attached policies / permissions to the created role

![image](https://user-images.githubusercontent.com/37842433/219373696-6a31f4f9-dc86-4c13-8167-a8d13f818e3a.png)


---

### EventBridge (Health Dashboard) & SNS Setup

- SNS Setup: SNS (Simple Notification Service) was setup with a topic and a subscription.

  - Topic
  
  ![image](https://user-images.githubusercontent.com/37842433/219375474-b58aa7b3-33ec-41ec-941d-fccd6d771622.png)

  
  - Subscription
  
  This was setup with an email verification
  
  ![image](https://user-images.githubusercontent.com/37842433/219375801-3a86057f-2fe0-4ddb-acea-35a5c571fd1c.png)
  
  
- EventBridge (Health Dashboard)

I created an EventBridge rule to get notified for AWS Health events in my account. The rule which can be seen below also generated a [main/_docs/assets/service-health-sns.json](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/main/_docs/assets/service-health-sns.json) file


![image](https://user-images.githubusercontent.com/37842433/219377414-d9383afb-08fc-45a8-92ae-58a5d8c29ca3.png)


---

### Open a support ticket and request a service limit

- Made a request to increase the limit of EC2-VPC Elastic IPs with the default at 5

![image](https://user-images.githubusercontent.com/37842433/219363826-31542e88-433d-4e85-8987-218e79d27f1c.png)

- Created a case for *VPC* limit type for a *Service limit increase*

Requested via *AWS Support portal* an increase from 5 to 10 as seen below

![image](https://user-images.githubusercontent.com/37842433/219364327-5ab974da-88b2-4310-9536-a74cf486ddab.png)

![image](https://user-images.githubusercontent.com/37842433/219365293-39b84623-1b24-4bbc-8a5e-e299d5dedf30.png)


- Email confirmation of Request limit increase

![image](https://user-images.githubusercontent.com/37842433/219367995-fdaf04cd-8ef3-4a62-ac88-4311e097f2a2.png)

- Request limit increase AWS Response

I received a response from *AWS Support* indicating that due to my new account, the request won't be possible till I am able to regularly utilise the resources.

![image](https://user-images.githubusercontent.com/37842433/219367666-6783ebde-da31-4aa9-a67a-7c8da01bd62f.png)

---

