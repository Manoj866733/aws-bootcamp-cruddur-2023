# Week 3 — Decentralized Authentication

This was the week 3 of the bootcamp. It was another changelling week with alot of new stuffs to learn. In this week I setup Amazon cognito and we changed the UI of our cruddur application.

## Setup Cognito User-pool
Using the Amazon Console, I was able to create a user-pool with the following steps.
 * In AWS console search for Amazon Cognito
 * Select create new user pool
 * In Cognito user pool sign-in options, Select only email as shown below
  
  ![image](https://user-images.githubusercontent.com/100923201/226099084-829667dc-471f-4ca5-9478-6b101f097f82.png)
 
 * In password policy select Cognito default and select no MFA in the bottom

![image](https://user-images.githubusercontent.com/100923201/226099200-d4caed08-62e1-4035-abfd-d13651b298c3.png)

 * In Configure sign-up experience page, Uncheck Self-registration and for Required attributes select the options as shown below.

![image](https://user-images.githubusercontent.com/100923201/226099336-419fa58f-de97-47e3-a6c4-ee60ccb5468a.png)

 * In Configure message delivery, Select Send email with Cognito
 * In Integrate your app page, We can set up app integration for our user pool with Cognito's built-in authentication and authorization flows. 
 * Finally, confirm the user-pool details and home page should be as shown below
 
 ![image](https://user-images.githubusercontent.com/100923201/226099447-7f93ae16-f28d-41ca-9dc6-fe6b123ae460.png)

# Install AWS Amplify library

## Setup Environment Variables for Frontend and Enabling Signing in

1. To interact with aws-cognito from the frontend, we need to install aws-amplify nodes. From the command line, I navigated to the frontend folder. Then I ran the following command:

*$ npm i aws-amplify --save

2. Then we need to add Env Vars in the docker-compose.yml file:
