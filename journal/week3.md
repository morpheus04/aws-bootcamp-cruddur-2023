# Week 3 — Decentralized Authentication


#### Table of Contents

+ [Required Homework](#required-homework)
  - [Setup Cognito User Pool](#setup-cognito-user-pool)
  - [Implement Custom Signin Page](#implement-custom-signin-page)
  - [Implement Custom Confirmation Page](#implement-custom-confirmation-page)
  - [Implement Custom Recovery Page](#implement-custom-recovery-page)
  - [Verify JWT Token server side to serve authenticated API endpoints in Flask Application](#verify-jwt-token-server-side-to-serve-authenticated-api-endpoints-in-flask-application)

  
  ## Required Homework
  
  
  
  ### Setup Cognito User Pool
  
  - `cruddur-user-pool` User Pool was setup
 
 ![image](https://user-images.githubusercontent.com/37842433/224728106-e6b89f1a-3bb5-4cd1-b8f5-fe6463b9e07a.png)

  - Amplify was also configured using `env vars` in the `App.js` file. Variable used were from the `AWS Cognito User Pool`
    - User pool ID
    - Client ID
    
  
  ---
  
  ### Implement Custom Signin Page
  
  - The Sign-in page was implemented to use an email (username) and password. [Commit link to b0117a](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/a856a71b5b64a5b45afe2be6c74ce3a7d19fcd9c#diff-b0117a4e4cca291e8ec64d0ef94b2c8dc3660d61718acaad43c292d80af75868)
  
  ![image](https://user-images.githubusercontent.com/37842433/224763653-4ee1d133-a130-4ab5-9ece-a3a05b67c1a6.png)

  
  ---
  
  ### Implement Custom Confirmation Page
  
  - Created Sign-up page for new user
  
  ![image](https://user-images.githubusercontent.com/37842433/224765536-b1e1f095-6fc7-4eee-9756-650cc1e7ea2c.png)
  
  Once signed up via the frontend login page, `Cognito User Pool` is also updated with new user. In our case, we now have 3 users created via the main signup page
  
  ![image](https://user-images.githubusercontent.com/37842433/224769165-972e3317-e75d-4cd0-9928-76381a217f1b.png)
 
  
  - Created Confirmation page once user has been created to confirm verification code sent on sign-up can be used to login
  
  ![image](https://user-images.githubusercontent.com/37842433/224766783-36e818bb-db03-48b6-a295-849cef0eda18.png)
  
  
  - User successfully authenticated after logging in
  
  ![image](https://user-images.githubusercontent.com/37842433/224767294-f978cccf-ae60-4282-93fd-484a7629cdd2.png)

   
  ---
  
  ### Implement Custom Recovery Page
  
  - Created Custom recovery page for lost or forgotten password / credentials
  
  ![image](https://user-images.githubusercontent.com/37842433/224767730-f52aaa27-30f8-4194-aad2-aab8f5787b68.png)
  
  - Password Recovery page
  
  Once user enters email address, a password recovery page is then shown to set new password
  
  ![image](https://user-images.githubusercontent.com/37842433/224768146-b6f6b588-0ba0-476c-a539-31f04fad41ce.png)
  
  - Password Reset confirmation
  
  ![image](https://user-images.githubusercontent.com/37842433/224768479-b681d5a6-7742-4635-9a59-b66b13d9cc1e.png)



  
  ---
  
  ### Verify JWT Token server side to serve authenticated API endpoints in Flask Application
  
  - This was implemented by creating a [cognito_jwt_token python file](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/3cec1c29746e8ba8ba9bbb39eee46b072703d602?diff=unified#diff-c4205e0c1fabfa8932a580cf9b109f3af4c9fe9c738868a9c7f8d83212db9c24) which passes the user token to the backend app whenever the user logins to perform any tasks on own page.
  
  - For the backend to run, the `Flask-AWSCognito` must be integrated via the [`requirements.txt`](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/3cec1c29746e8ba8ba9bbb39eee46b072703d602?diff=unified#diff-55d5801c5f315ed423b03e986f4ecf1d3915c097ac8c66c733f0e4cbc17cfee3) file. This will allow `AWS Cognito` utilise the backend along with the JWTs.
