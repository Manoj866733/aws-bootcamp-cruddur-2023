# Week 2 — Distributed Tracing

## Journal Entry - Week 2: Distributed Tracing and Observability

Week 2 covered the next stage of our bootcamp process, which was adding components of observability and tracing into our application (Crudder) and testing all components of the app to ensure its readiness for deployment. It was the toughest and challenging week so far. It took 2 weeks to complete this session.

## Honeycomb
Honeycomb is a distributed tracing & observability platform to help understand & debug complex systems.

* I completed all the task as shown in the livestream
* I confirmed trace data is captured in Honeycomb.io

![image](https://user-images.githubusercontent.com/100923201/225388213-4731117e-eaef-4464-a7e8-55beebb0209f.png)

## XRAY
AWS X-Ray is a tracing service that helps to analyze & debug distributed applications.

## Install AWS XRay SDK (boto3)

1. Add to requirements.txt

 * pip install aws-xray-sdk
 * pip freeze >> backend-flask/requirements.txt

2. Add Middleware configuration to your flask app.py


3. Add x-ray-json to your json directory in /aws.json/xray.json:
 
![error 1 fixed](https://user-images.githubusercontent.com/100923201/225391795-720439a9-4527-4728-8e0f-9aee05837d4c.png)


4. Create a group and a sampling rule

 * aws xray create-sampling-rule --cli-input-json file://aws/json/xray.json

![3](https://user-images.githubusercontent.com/100923201/225391726-727c053c-38b8-4428-abcd-5136c299a08b.png)

![Screenshot 2023-03-08 201516](https://user-images.githubusercontent.com/100923201/225392108-d107f7da-b555-4f57-b62d-0d04a27cb3fe.png)


5. Add daemon service to docker compose in docker-compose.yml

6. Trace Maps:

![traces](https://user-images.githubusercontent.com/100923201/225392450-8a984561-700b-42d5-9155-54d3aff132e5.png)

![TRACES is successfull](https://user-images.githubusercontent.com/100923201/225392503-56492a54-a50f-46db-af6d-44bce772fc26.png)

![trace map](https://user-images.githubusercontent.com/100923201/225392584-09bd5bc0-3d3b-4b63-95ef-fe65f4d7e1d6.png)


## Configure Cloudwatch logs

 * I completed all the steps provided to implement Cloudwatch logging in AWS
 * Used WatchTower as a log handler in AWS CloudWatch
 * Used Logging to manage logs generated
 * Confirmed Logs stream are captured in AWS CloudWatch

![log stream](https://user-images.githubusercontent.com/100923201/225393187-0457d979-149c-4ab8-9732-7a0fb81ba346.png)

## Integrate Rollbar

1. Install blinker, rollbar

2. Set rollbar access token from rollbar website

3. Export rollbar access token and add it to your docker-compose.yml

4. Import rollbar libraries to app.py

5. Add configuration to app.py

![rollbar](https://user-images.githubusercontent.com/100923201/225394097-8bc4e0a5-84df-4aec-b3b9-86c1201f79a7.png)

![items for rollbar](https://user-images.githubusercontent.com/100923201/225394161-c7283393-4d9c-4c89-b198-a6a13fc609a0.png)

![rollbar test](https://user-images.githubusercontent.com/100923201/225394240-6bc5f892-85f0-4f26-bc61-70cc7a6113b1.png)

## Errors faced 
1. While adding xray.json file I was getting an error. "Error parsing parameter '--cli-input-json': Unable to load paramfile file://aws/json/xray.json: [Errno 2] No such file or directory:''aws/json/xray.json'"  

![error 1 aws json](https://user-images.githubusercontent.com/100923201/225395844-f1ce7394-4fd8-4e02-bd2b-09a94a8566df.png)

To fix this I changed the name to aws.json and created a new terminal and enter the same code again it worked 

![error 1 fixed](https://user-images.githubusercontent.com/100923201/225396209-35e8adb1-cf0c-4815-b2ac-f7947224ac19.png)

![Setup AWS X-Ray Resources](https://user-images.githubusercontent.com/100923201/225396244-827b0d95-c3f1-4c87-98ac-2138161f724d.png)


2. Backend is not served. checked in logs getting an value error  invalid endpoint: https://logs..amazonaws.com/

![Screenshot 2023-03-14 210050](https://user-images.githubusercontent.com/100923201/225398252-fec059f2-2cfe-4eec-ad53-947661efc689.png)
 
![error 1 -ports](https://user-images.githubusercontent.com/100923201/225396432-aee6c1c5-19aa-43c4-a9ef-5c3e3f55f155.png)

![discord 1 error](https://user-images.githubusercontent.com/100923201/225396484-f8b9cd54-f447-4a00-845d-e5bc51da51f3.png)

AWS_DEFAULT_REGION variable was not set to my environment and i set it manually. Checked in logs and added environmental variables  

![image](https://user-images.githubusercontent.com/100923201/225396908-0e18f769-cc08-4e88-bde9-ad6012b96fa2.png)

![backend port working](https://user-images.githubusercontent.com/100923201/225396986-26a6974a-84e8-4b49-a507-ae5b3ca0f675.png)



## Adding ports in .gitpod.yml

https://github.com/Manoj866733/aws-bootcamp-cruddur-2023/blob/main/.gitpod.yml

## to set tags: use this two commands

git tag week-2
git push --tags

once this is done we can see tags in github main branch
