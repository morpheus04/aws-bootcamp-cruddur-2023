# Week 6 — Deploying Containers


#### Table of Contents

+ [Required Homework](#required-homework)
  - [Provision an Elastic Container Repository (ECR) via the AWS CLI command](#provision-an-elastic-container-repository-ecr-via-the-aws-cli-command)
  - [Create docker container images and push them to Elastic Container Repository](#create-docker-container-images-and-push-them-to-elastic-container-repository)
  - [Create file to provision ECS task definitions for Fargate](#create-file-to-provision-ecs-task-definitions-for-fargate)
  - [Provision Fargate services for individual apps via AWS CLI command](#provision-fargate-services-for-individual-apps-via-aws-cli-command)
  - [Provision Security Groups, Target Groups & Application Load Balancer via the AWS CLI](#provision-security-groups-target-groups--application-load-balancer-via-the-aws-cli)
  - [Connect to provisioned Fargate cluster via Sessions Manager](#connect-to-provisioned-fargate-cluster-via-sessions-manager)

  
  ## Required Homework
  
  
  
  ### Provision an Elastic Container Repository (ECR) via the AWS CLI command
  
  - Created repositories for main app and both frontend & backend apps by setting the `env vars` and using the AWS CLI
  ```
  aws ecr get-login-password --region $AWS_DEFAULT_REGION | docker login --username AWS --password-stdin "$AWS_ACCOUNT_ID.dkr.ecr.$AWS_DEFAULT_REGION.amazonaws.com"
  ```
  
  ![image](https://user-images.githubusercontent.com/37842433/232246016-ff376aa6-b452-4e9d-8981-32d193a551f7.png)

   
  ---
  
  
  ### Create docker container images and push them to Elastic Container Repository
  
  - Create docker images for each app and deployed them to corresponding ECRs. E.g. Backend-flask ECR with its latest image
  
  ![image](https://user-images.githubusercontent.com/37842433/232246222-157ebfbf-57a9-4fe8-a8a5-a3a080d3aa86.png)

  - Cruddur-Python image
  
  ![image](https://user-images.githubusercontent.com/37842433/232246246-e775c28f-d9a6-4981-9e7e-d7c41f01068a.png)

  
  ---
  
  
  ### Create file to provision ECS task definitions for Fargate
  
  - In order for task definitions to be created, task roles had to be created with Trusted entities
  
  ![image](https://user-images.githubusercontent.com/37842433/232246574-fc7762e7-5b0e-4184-b571-917b03dd4182.png)
  
  
  - [Backend Task Definition file can be found here](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/cdb66ff6cca84945d69f9e03b9b7078a9c422813/aws/task-definitions/backend-flask.json)
  
  - [Frontend Task Definition file can be found here](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/cdb66ff6cca84945d69f9e03b9b7078a9c422813/aws/task-definitions/frontend-react-js.json)

  - Task Definitions
  
  ![image](https://user-images.githubusercontent.com/37842433/232247049-f66cfa6d-e0ac-4f13-b29b-68f48adb2d6d.png)
  
  
  - Tasks (Running)
  
  ![image](https://user-images.githubusercontent.com/37842433/232247392-9a0e7881-6eac-4607-b7b0-40e14cddd8d5.png)


 
 
  ---
  
  
  ### Provision Fargate services for individual apps via AWS CLI command
  
  - [Backend app Service](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/cdb66ff6cca84945d69f9e03b9b7078a9c422813/aws/json/service-backend-flask.json)
  
  ![image](https://user-images.githubusercontent.com/37842433/232247145-76594fe4-5aa5-45ca-8ea5-35c52adc12a9.png)

  
  ---
  
  
  ### Provision Security Groups, Target Groups & Application Load Balancer via the AWS CLI
  
  - Created Security Groups for the ECS Service
  
  ![image](https://user-images.githubusercontent.com/37842433/232247288-47c664a5-b185-4912-a8fe-db36631cc4ba.png)
  
  - Created Security Group for Load Balancer
  
  ![image](https://user-images.githubusercontent.com/37842433/232247326-9d5f40cf-192e-400f-b4e5-255f93d801a9.png)


  ---
  
  
  ### Connect to provisioned Fargate cluster via Sessions Manager
  
  - Using the Sessions Manager plugin in the AWS CLI, connection to each of the instances provisioned from the tasks was possible
  
  ![image](https://user-images.githubusercontent.com/37842433/232247510-57869722-8628-411e-8e7d-e8ab68fb83d8.png)
  
  ![image](https://user-images.githubusercontent.com/37842433/232247522-b2761ee3-cbf0-4498-b6d2-8e543fb28584.png)


