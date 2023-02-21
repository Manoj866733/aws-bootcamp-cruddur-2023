# Week 0 — Billing and Architecture

##Synopsis

This journal consists of the tasks completed in week-0 of AWS Free Bootcamp 2023 organized by Andrew Brown and his Team. In this week, we started with setting up the requirements that are needed to start the ‘Cruddur Project’.

##Pre-Requisites:

Before starting this Cloud Project Bootcamp we have to ready with some requirements. For detailed explanation check the playlist by Andrew Brown and his team here : youtube.com/playlist?list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv

Now, Let's talk about the services we're going to work in this bootcamp!

we have to register for the following services:

Create a Github Account, Copy Andrew's repository with the right formatting of the repo and make it as Public.
Create a Gitpod account and install the extension for your browser.
Create Github CodeSpace
Create an AWS account ( Whether it is Free tier or premium, it's upto user)
Create Lucidchart ( Hint - In this week, we're going to work here)
Create Honeycomb.io account
Create Rollbar account
Week-0 Billing, Architecture & Security
Week-0 Live Session conducted By AWS Cloud project Bootcamp Organizer Andrew, and his guest lecturers - Shala Warner, Chris Williams and Margaret Veltierra.

What are they discussed in this Live Session ?

This was mainly focused on Billing and Architecture

We learnt how to understand the client’s requirements, how to segregate tasks and gather the requirements for the project.
Different architectures – monolithic and microservice architecture.
Introduction to AWS console, Gitpod console, GitHub repositories.
Understanding about Conceptual, Logical and Physical Diagrams.
Got to know about TOGAF Architecture.
C4 models.
How to create diagrams in Lucid Charts.
Hands on example for Napkin Diagram.
##Tasks/Challenges to be Completed for week-0

**1. Create an IAM user,role, add mfa.**

Steps to be followed inorder to create an IAM user, add multi-factor authentication. Login as a root user into AWS account.

Search for IAM service and go to Users.
Create a new User by giving the appropriate (Admin) permissions. After that to set MFA you can go to particular User -> Security Credentials -> Enable MFA.
Fill the required details and Scan QR code from the authentication app in your mobile. (Here you need to install authentication application in your mobile to connect it with your IAM User).
Enter two MFA Codes when asked and your MFA is set.
Creat an IAM Role

From IAM click on Roles -> Create role.
Choose Entity Type as per your project, I personally chose AWS Services for EC2 Use case.
Added permission policy as Security Audit.
Then give role name and Tags and click on Create role. If you're getting any error or facing any challenges while creating user or role, it means your'e not authorized to create a user/role with your credentials.Upgrade to root account or get permission from root user to create a role/user.


**2. Install AWS CLI in GitPod**

Command to Install AWS CLI:
curl -fSsl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

unzip -qq awscliv2.zip

sudo ./aws/install --update

rm awscliv2.zip

In this command we're using "sudo". If you're a root user you don't need to add sudo. it is used to run the command with elevated privileges.


**3. Create a Billing Alarm**

There are 2 ways to set the billing alerts.
Using Budget.
Using Cloudwatch Alarm. In this case, you need to create an alarm on us-east-1 region (since it is the only region you can create an alarm for free-tier). You can create up to 10 free cloudwatch alarms with free-tier.
Those 2 alarms will be helpful to identify if you are underspending/overspending. Also we will receive an e-mail whenever the limit(We can mention as much as we want) exceeds.

AWS Calculator : https://calculator.aws/#/
This is a tool where you can estimate the cost of any service based on the client requirements without actually using it.


**4. Re-create Conceptual Diagram in Lucid-Charts**

I'm new to lucid chart and I found it very hard to handle. But somehow Andrew video on Lucid Chart saved me.

A Snapshot for quick reference. 
https://lucid.app/lucidchart/98e85b6a-7457-4f1d-98d3-99198f46a6e1/edit?viewport_loc=11%2C234%2C1793%2C757%2C0_0&invitationId=inv_e7e84056-34e5-4105-ba9b-2d35477b08a2

![Manoj lucidchart diagram](https://user-images.githubusercontent.com/100923201/220348709-772f0bba-6f65-4f16-912d-22b0a12b7ea9.jpg)


**5. Create a Napkin Design**

This is my Napkin Design depicting that the User upload application/website in the cloud where it will pass the Authentication and segregate via Load Balancer. AppSync provide the interface for real-time AND as a backend which is connected to the DataBase for storing the information that is also connected with the Appsync. 

![nappin design](https://user-images.githubusercontent.com/100923201/220346451-655bb4fe-d381-4123-bb3d-5a2d61a0e414.jpg)

https://lucid.app/lucidchart/91296fb5-071e-4766-89f3-9665eee3e929/edit?viewport_loc=-392%2C-95%2C1791%2C756%2C0_0&invitationId=inv_4d5a65c2-bd51-48ca-aa40-9bf4d87beb48

![napkin design in Lucid chart](https://user-images.githubusercontent.com/100923201/220350144-199ec7bb-44fc-44b8-bdc4-d22ffe0cc546.jpg)



**6. Quiz on Pricing and Security**

It's very easy to solve the quiz after watching Chirag Nayyar's video about the Pricing Considerations and Ashish Rajan's video about Security Considerations. Those videos really help me understand the basics related to Pricing and Security and to clear the Quiz. To find the links to these videos open Andrew and his team playlist or open this!

Chirag's Pricing Video : https://youtu.be/OVw3RrlP-sI

Ashish's Security Video : https://youtu.be/4EMWBYVggQI




_Summary:_

Watched Week 0 - Live Streamed Video	✔	

Watched Chirag's Week 0 - Spend Considerations	✔	

Watched Ashish's Week 0 - Security Considerations	✔	

Recreate Logical Architectual Diagram in Lucid Charts	✔	

Recreate Conceptual Diagram in Lucid Charts	✔	

Create an Admin User	✔	

Use CloudShell	✔	

Generate AWS Credentials	✔	

Installed AWS CLI	✔	

Create a Billing Alarm	✔	

Create a Budget	✔	
