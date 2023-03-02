# Week 1 — App Containerization

## Journal Entry - Week 1: Application Containerization ##

Week 1 covered the next stage of our bootcamp process, which was containerization of our application (Crudder) and testing all components of the application to ensure its readiness for deployment. In this week I learned many things including notification feature for (frontend and backend) and also installed Dynamo DB and postgres in to our application.

## Required Homework ##
**Containerize Backend and Frontend Application**
In containerizing our application, we needed to use a package manager called "NPM" to automate the installation and management of our software packages. we did the following for our application:

# Frontend: #

cd into frontend and initating Node Package Manager (NPM), below are the codes.

> cd frontend-react-js        
> npm i                       
 
we confirmed that our frontend application was in good shape.
Ports were open and made public   (3000 is the port)

![image](https://user-images.githubusercontent.com/100923201/222405953-b5f68a74-e11b-4f33-9ced-597ccbf22c5f.png)

The frontend accessible over the web

![image](https://user-images.githubusercontent.com/100923201/222407663-f60a7dff-22a8-40bf-880e-74b9576db7dd.png)

# Backend: #

![image](https://user-images.githubusercontent.com/100923201/222415643-8c37ae52-da6c-4851-b91e-604f2a527c11.png)


* Exported the frontend and backend url as an enviromental variable
* we confirmed that our backend application was in good shape.
* Ports were open and made public      (4567 is the port)
* The backend accessible over the web **/api/activities/home**

![image](https://user-images.githubusercontent.com/100923201/222412080-2a88a6dc-615d-49ee-b179-11a45c02736f.png)

We then proceed to automate the processing of building our application by using a Dockerfile to automate the containerization of our application.
In gitpod, install an extension for docker. Then create an new file "dockerfile" in backend-flask and add the below scripts in to it.

Backend:
> * cd backend-flask
> * touch Dockerfile
> * cd backend-flask/Dockerfile

We are then adding the below codes into our Dockerfile


> * FROM python:3.10-slim-buster
> * WORKDIR /backend-flask
> * COPY requirements.txt requirements.txt
> * RUN pip3 install -r requirements.txt
> * COPY . .
> * ENV FLASK_ENV=development
> * EXPOSE ${PORT}
> * CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]

Frontend:

> * cd frontend-react-js
> * touch Dockerfile
> * cd frontend-react-js/Dockerfile

We are then adding the below codes into our Dockerfile

> * FROM node:16.18
> * ENV PORT=3000
> * COPY . /frontend-react-js
> * WORKDIR /frontend-react-js
> * RUN npm install
> * EXPOSE ${PORT}
> *CMD ["npm", "start"]

After creating our Dockerfile, we proceeded to building our container using the Dockerfile we created.

>* docker build -t frontend-react-js ./frontend-react-js       # Building the frontend container
>* docker build -t backend-flask ./backend-flask               # Building the backend conatiner

After building our container, we run the container

>* docker run -p 3000:3000 -d frontend-react-js         # Running the frontend container in background mode with specific port for access
>* docker run -p 4567:4567 -d backend-flask             # Running the backendend container in background mode with specific port for access

We confirm that our container is now running and frontend image built

>* docker ps
>* docker images
>* docker ps -a

Next step was to create a Docker-Compose file to handle mutiple containers as this will help us automate the need to build the frontend and backend simulteaneously rather than the manual method we used earlier through Dockerfile

At the root directory of our repository/project, we created a docker compose file

>* cd aws-bootcamp-crudder-2023
>* touch docker-compose.yml

We then added the following YAML code into our created docker-compose file.    
you can get the codes from the below link:

https://github.com/Manoj866733/aws-bootcamp-cruddur-2023/blob/main/docker-compose.yml

The above YAML script now allow us automate the builiding and running of our frontend and backend container.

>* docker-compose up

After **docker compose up** command was executed, we can confirm that our frontend and backend applications are both running on their respective ports 3000 and 4567.


## Updating the backend and frontend code to add notifications functionality

Backend:

We created a Notifications file in our backend to handle our backend activities.

![image](https://user-images.githubusercontent.com/100923201/222418891-3d271df4-7d3a-4cae-b659-2bb24e86c024.png)


Frontend:

We created a Notifications Feed Page file in our frontend to provide a UI for our notifications page

![image](https://user-images.githubusercontent.com/100923201/222419574-697518e6-ca33-4f8a-b588-e58cff916b6f.png)


# DynamoDB Local and PostgreSQL

We are addeding a dynamodb database and postgres to reference to our containers.
Make sure to configure AWS with gitpod

DynamoDB

![image](https://user-images.githubusercontent.com/100923201/222420290-bbc98bf9-c6a7-4174-81b4-178e883b0a99.png)


Postgres

![image](https://user-images.githubusercontent.com/100923201/222420463-e4de5810-ecde-4dcd-bf6e-340755eede79.png)

Use the below link to add the codes to our table.
https://github.com/100DaysOfCloud/challenge-dynamodb-local

I got an error while using the above link, There seems to be an issue with the code on **get records.
**aws dynamodb scan --table-name Music --query "Items" --endpoint-url http://localhost:8000

Then we need to install postgres extenstion in to our gitpod file. And also add the extension to our gitpod.yml file

![image](https://user-images.githubusercontent.com/100923201/222421672-ae5f7bf9-a0f5-41ae-805a-6eef5a344988.png)


Once postgres extension installing is completed. Connect to our database explorer.

![image](https://user-images.githubusercontent.com/100923201/222422527-0496e8cd-5746-4a35-b4d3-e6847952c4c9.png)

![image](https://user-images.githubusercontent.com/100923201/222422672-d6a3bf93-1d96-4cbd-a4d2-d5e08cfb3528.png)

Then added a command to confirm the client for postgres.

> * psql -U postgres --host localhost

![output final](https://user-images.githubusercontent.com/100923201/222423145-171e108f-7df9-4a2f-8a97-dea7b0c84967.jpg)

![output](https://user-images.githubusercontent.com/100923201/222423479-3c80dbb0-4b58-412b-929f-b9ee6b6f4e41.jpg)

*final output
![2](https://user-images.githubusercontent.com/100923201/222423838-622d5a4f-26d3-4222-bccb-a9f66cf75b29.jpg)


## Challenges Faced

While creating a dockerfile for backend. I was not getting the endpoint in the browser. I was getting a 404 error.
![image](https://user-images.githubusercontent.com/100923201/222443147-f10724a0-861b-4421-98df-f26a4dad1955.png)

* I made few mistakes in the naming like for activities i wrote activity and for Notifications i wrote notification.
* I left the extenstion .py and .js 
* corrected my mistakes by watching Andrew's videos few time.
* Added **/api/activities/home** in the URL and now I got the endpoint of backend.
![image](https://user-images.githubusercontent.com/100923201/222443444-6fd55c67-1d89-44d9-8a64-9f189e0af27b.png)

* While creating the notification, I was not getting the notifications tab in cuddr app. The UI seems to be incomplete.  
* Then, I signed in to my account and now I can see the notification tab in cuddr
![image](https://user-images.githubusercontent.com/100923201/222444633-a2911861-b402-43ff-8cef-22cf96ca8da7.png)


* The major issue I faced during week 1 homework challenge was I'm unable to connect to the postgres database. I have installed postgres extension and the connection type says its successfull but I'm not getting the details in database explorer section. The tables and data were missing from the database explorer section, 
Please find the attached image for your references.

![image](https://user-images.githubusercontent.com/100923201/222445423-70d4abb8-5bd1-4386-b642-c45f019d6c93.png)


Troubleshooting steps are, I stopped the docker-compose.yml file and uninstall postgres extension. I restarted the gitpod account and initiated docker compose up. Opened all the ports and installed postgres extension again. Added the extension in to our gitpod.yml file. Then went to database explorer extension and select new connection, This time it was successfull, I can now see the postgres database. 

![output final](https://user-images.githubusercontent.com/100923201/222446826-edd46132-0c64-404a-b6c3-2bc756e10756.jpg)




# Definition of terms #
### Containerization: ###
Containerization is a way of packaging software applications and their dependencies into a standalone, portable unit called a container. Containers provide a consistent and isolated environment for applications to run in regardless of the underlying infrastructure. This means that applications can be easily moved between different environments, such as from a developer's laptop to a test environment or a production server, without the need for additional configuration or setup.

### Container: ###
Container is a standard unit of software that packages application codes and its dependencies into a single object. It is a layer of images with a linux baseline.

### dockerhub: ###
It is a container registry provided by docker where we can host our own container images or we can also share our container images.

### Package Manager: ###
A package manager is a tool that automates the process of installing, upgrading, configuring, and removing software packages. It manages the dependencies between packages, ensuring that all required software is installed and configured correctly. Package managers are used to simplify the installation and management of software on a system.

### Docker: ###
Docker is a PAAS product that uses OS-level virtualization to deliver software in packages called containers. It is a software platform that simplifies the process of building, running, managing and distributing applications.

### Dockerfile: ###
A Dockerfile is a text file that contains instructions for building a Docker image. An image is a packaged, standalone executable software package that includes everything needed to run an application, including the application code, libraries, and other dependencies. The Dockerfile provides a set of instructions for the Docker engine to create an image. It contains information such as what base image to use, what software packages to install, what files to copy into the image, and what commands to run. The Dockerfile can also set environment variables and define other configuration options. Once the Dockerfile is created, it can be used to build an image using the Docker build command. The resulting image can then be used to create and run containers that contain the application. Overall, a Dockerfile is a way to automate the creation of Docker images, making it easier to manage and deploy applications in containers.






