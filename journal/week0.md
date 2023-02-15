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


## Required Homework (Instructional Homework)

### Lucid Diagrams
|Task|URL|Screenshots (Images)|
|----|-----|-------|
|Recreate Conceptual Diagram in Lucid Charts or on a Napkin|[Conceptual Diagram](https://lucid.app/lucidchart/621ecb99-b13c-41be-9775-85153ace2582/edit?viewport_loc=-399%2C65%2C2219%2C1089%2C0_0&invitationId=inv_6eecf645-1a68-4568-a410-ccb1bb77fb4e)|![image](https://user-images.githubusercontent.com/37842433/219058172-0555637e-dbfd-4c93-a8f7-57d4737b1ff2.png)|
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



## Homework Challenges

### Budgets & Billing Alarm

#### <ins>Create a Budget</ins>

- *Cloud-BootCamp-Budget*

I created threshold alerts created dependent on the % of actual spend vs set amount. This can be seen in the diagrams below

![image](https://user-images.githubusercontent.com/37842433/219121541-70c05e71-f95f-45c5-8740-ea0bb65c6858.png)

An extract of the code showing the creation of 4 threshold alerts (20% - 80%) as referenced in my repo

[main/aws/json/budget-notifications-with-subscribers.json](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/main/aws/json/budget-notifications-with-subscribers.json)
