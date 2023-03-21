# Week 4 — Postgres and RDS

#### Table of Contents

+ [Required Homework](#required-homework)
  - [Create RDS Postgres Instance](#create-rds-postgres-instance)
  - [Implement Security Group for RDS](#implement-security-group-for-rds)
  - [Bash scripting for common database actions](#bash-scripting-for-common-database-actions)
  - [Install Postgres Driver in Backend Application](#install-postgres-driver-in-backend-application)
  - [Connect Gitpod to RDS Instance](#connect-gitpod-to-rds-instance)
  - [Create Cognito Trigger to insert user into database](#create-cognito-trigger-to-insert-user-into-database)
  - [Create new activities with a database insert](#create-new-activities-with-a-database-insert)

  
  ## Required Homework
  
  
  
  ### Create RDS Postgres Instance
  
  - Provisioned a AWS RDS Postgres instance
  
  ![image](https://user-images.githubusercontent.com/37842433/226619584-532d6bad-5c6a-49d8-b76d-ac67ab6579db.png)
  
  ![image](https://user-images.githubusercontent.com/37842433/226620213-bd6a7d86-a30d-44a0-b780-d8ed747d6b0f.png)

 
  ---
  
  
  
  
  ### Implement Security Group for RDS
  
  - Security Group was created to allow for inbound traffic via the Postgres port `5432` which from the GITPOD endpoint
  
  ![image](https://user-images.githubusercontent.com/37842433/226621244-db3c75bf-691d-4a48-abf2-bc245c4ba6d2.png)

  
  ---
  
  
  
  
  ### Bash scripting for common database actions
  
  - Created bash scripts for e.g. inserts, create and activities that require database interactions
     - [home](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/713810c29e226fd36be2259d4d8acdc44ac56458?diff=unified#diff-5c1a2b6b47243795c31c78ab3d3c6ff2032c31a174f9f58a7dc94313f86f239c)
     - [create](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/713810c29e226fd36be2259d4d8acdc44ac56458?diff=unified#diff-bde677e0d6c2c0d57cc752a9bd9b943e80a7dbafd5f754ad09d2fa39190e5ac9)
     - [object](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/713810c29e226fd36be2259d4d8acdc44ac56458?diff=unified#diff-27a3294f656bc0a49186c9e0fe9b1fc0cc34d45732267051e8de4b5e8282bd2a)
     - [schema](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/713810c29e226fd36be2259d4d8acdc44ac56458?diff=unified#diff-bbc12a1f400fea71904f24b48cd2032ec91f812c051c3957b664e36b4fc04887)
  
  
  ---
  
  
  
  
  ### Install Postgres Driver in Backend Application
  
  - Setup Postgres client / driver
    - Added the RDS endpoint via an env var to GITPOD
    
    ```
      backend-flask:
    environment:
      CONNECTION_URL: "${CONNECTION_URL}"
    ```
    
    - Added the postgres drivers to the `requirements.txt` file
    
    ```
    psycopg[binary]
    psycopg[pool]
    ```
   
    - Installed the drivers using `pip install -r requirements.txt`
  
  ---
  
  
  
  
  ### Connect Gitpod to RDS Instance
  
  - To connect the RDS Postgres instannce to GITPOD, an AWS Security Group had to be created
  
  ![image](https://user-images.githubusercontent.com/37842433/226625094-871dad3d-e256-437a-81ca-b3ba26d425df.png)
  
  - Added the endpoint into the `docker-compose.yml` file via the entry below, where `PROD_CONNECTION_URL` is the AWS RDS endpoint
   
    ```
      backend-flask:
      environment:
        CONNECTION_URL: "${PROD_CONNECTION_URL}"
    ```

 - Script to automatically connect GITPOD to the AWS RDS instance
   - [Map GITPOD endpoint to Security Group & Autoconnect to RDS Instance](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/5ef45f448695260fb74918aa73004f206a7c7c67)
 
 - [Updated AWS Security Group automatically based on the backend  and map the GITPOD endpoint to the AWS RDS Security Group](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/cd79503a4e36702eaf3a8d73b9466605bbeb46f1)
 
 ```sh
     command: |
      export GITPOD_IP=$(curl ifconfig.me)
      source "$THEIA_WORKSPACE_ROOT/backend-flask/db-update-sg-rule"
 ```

 ```sh
 --security-group-rules "SecurityGroupRuleId=$DB_SG_RULE_ID,SecurityGroupRule={Description=GITPOD,IpProtocol=tcp,FromPort=5432,ToPort=5432,CidrIpv4=$GITPOD_IP/32}"
 ```

  ---
  
  
  
  
  ### Create Cognito Trigger to insert user into database
  
  - [Created Lambda function for this task](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/9fa129e37e387a64a650aa17d60aed435c493e56#diff-b338a2fe837c23358ed4fb5a07bf50dc053d855a802dec96e333c3156b05cafc)
  
  ![image](https://user-images.githubusercontent.com/37842433/226631966-ed82c544-afbb-4298-875a-fe2a41a0d8e6.png)

  - Newly created user after signup via the Cruddur page as well as validation and confirmation of email (username)
  
  ![image](https://user-images.githubusercontent.com/37842433/226635152-43071efd-3fc1-4dcb-a224-5e230fb61582.png)

  
  ---
  
  


  ### Create new activities with a database insert
  
  - Newly created posts via the Cruddur page
  
  ![image](https://user-images.githubusercontent.com/37842433/226635405-585af84a-725d-47e4-ac7d-1fea8b4c480f.png)
  
  ![image](https://user-images.githubusercontent.com/37842433/226635441-bbe10cc9-17a0-4663-8307-517736dd009e.png)
  
  
  - Post Creation of activity (by checking the database)
    
    ![image](https://user-images.githubusercontent.com/37842433/226635716-3a9b7386-dc3c-488a-8ad5-990dca2a5494.png)

  
