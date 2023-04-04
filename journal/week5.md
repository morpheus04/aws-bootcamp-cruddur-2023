# Week 5 — DynamoDB and Serverless Caching


#### Table of Contents

+ [Required Homework](#required-homework)
  - [Learn about Data Modelling (Single Table Design) for NoSQL](#learn-about-data-modelling-single-table-design-for-nosql)
  - [Implement SQL Scripts](#implement-sql-scripts)
  - [Implement Pattern Scripts for Read and List Conversations](#implement-pattern-scripts-for-read-and-list-conversations)
  - [Implement Update Cognito ID Script for Postgres Database](#implement-update-cognito-id-script-for-postgres-database)
  - [Implement Patterns for Listing Messages](#implement-patterns-for-listing-messages)
  - [Implement Patterns for Creating Messages](#implement-patterns-for-creating-messages)
  - [Implement Pattern for Updating a Message Group using DynamoDB Streams](#implement-pattern-for-updating-a-message-group-using-dynamodb-streams)

  
  ## Required Homework
  
  
  
  ### Learn about Data Modelling (Single Table Design) for NoSQL
  
 
  :memo: **Note:** `NoSQL Data Modelling is a model that is not reinforced by a Relational Database Management System (RDBMS).
  Therefore, the model isn’t explicit about how the data relates i.e. how it all connects together.`
  
  - The use of DynamoDB which is a NoSQL Database allows for unstructured data / items.
  - Benefits of a single-table design in DynamoDB which includes;
     - Performance improvement by making a single request to retrive all needed items.
     - Reduced setup of metrics and alarms for seperate tables as a single set of netrics / alarms are all that are needed in this instance
  - Techniques such as the use of an index table, composite keys which are incredibly useful when ordered keys are used
  
 
  ---
  
  
  
  ### Implement SQL Scripts
  
  - To be able to create, load or view data, [These scripts can be found here](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/3b0eed3c6445bf6f8235eb7f192dc2f32b2fef14?diff=unified)
  
  
  ---
  
  
  
  ### Implement Pattern Scripts for Read and List Conversations
  
  - Displaying conversations in the database required creating scripts that will output the many user conversations. [These can be found here](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/df89a95ea6d03f87332fdd50efeb72a5d96bea5b)
 
 ![image](https://user-images.githubusercontent.com/37842433/229145255-55343ef5-0ab2-4acc-a858-cd4f4525000a.png)  ![image](https://user-images.githubusercontent.com/37842433/229145352-17c710e2-42cf-42bd-8ca3-4a141e3178e9.png)


  
  
  ---
  
  
  
  
  ### Implement Update Cognito ID Script for Postgres Database
  
  
  - For the Cognito User ID to be stored in the Postgres DB, [a script](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/3aee5c4b737568bfaa894052b203467f6325d43e/backend-flask/bin/db/update_cognito_user_ids) was created to allow for the table `users` to be updated
  
  ![image](https://user-images.githubusercontent.com/37842433/229146735-1b83a90c-bd53-4785-aa9f-33cd57d9b5a2.png)
  
  
  ---
  
  
  
  ### Implement Patterns for Listing Messages
  
  - For messages to be displayed betwen users, scripts were created which pulled data from DynamoDb and displayed in a structured manner
      - [Get](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/3b0eed3c6445bf6f8235eb7f192dc2f32b2fef14/backend-flask/bin/ddb/get-conversation)
      - [List](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/3b0eed3c6445bf6f8235eb7f192dc2f32b2fef14/backend-flask/bin/ddb/list-conversation)
  
 ![image](https://user-images.githubusercontent.com/37842433/229150909-74111584-1cf5-4e8e-9aea-378138d9c4f7.png)
 
 ![image](https://user-images.githubusercontent.com/37842433/229150697-4c9a2e11-d76e-4588-a07c-4ec275778718.png)



  
  ---
  
  
  
  ### Implement Patterns for Creating Messages
  
  - The use of indexes `(Partition & Sort keys)` were needed to allow for these patterns of creating messages
  - The creation of messages to be stored in the prod DynamoDB `cruddur-message` table was implemented by creating a [script](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/0586a5c9ee5f89c2ccf8b7b9fb088dc9cfb7fca2/backend-flask/bin/ddb/schema-load) to load the DynamoDB schema.


![image](https://user-images.githubusercontent.com/37842433/229153638-299d182d-d4b0-409f-a44c-8e2a2aecd406.png) | ![image](https://user-images.githubusercontent.com/37842433/229153711-a52637a1-ef08-483c-a4fa-0d2f1ba8ffee.png)



  
  ---
  
  
  
  ### Implement Pattern for Updating a Message Group using DynamoDB Streams
  
  - The use of indexes `(Partition & Sort keys)` were needed to allow for these patterns of updating messages
  - The updating of messages to be stored in the prod DynamoDB `cruddur-message` table was implemented by creating a [AWS Lambda function](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/blob/main/aws/lambdas/cruddur-messaging-stream.py). This function gets triggered once a user sends a new message to another user.


![image](https://user-images.githubusercontent.com/37842433/229153638-299d182d-d4b0-409f-a44c-8e2a2aecd406.png) | ![image](https://user-images.githubusercontent.com/37842433/229153711-a52637a1-ef08-483c-a4fa-0d2f1ba8ffee.png) | ![image](https://user-images.githubusercontent.com/37842433/229153759-efa5a266-29c9-4fa4-9737-32fcd53730e4.png)

