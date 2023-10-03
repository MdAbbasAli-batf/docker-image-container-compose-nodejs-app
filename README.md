## A demonstration of Docker Image build and running container to implement a simple 3 tier architecture.

- frontend (React)

- backend (nodejs REST API)

- db (mongodb)



frontend will be able to access the mid-tier (backend)
The backend (mid-tier) will be able to access the db


#### In order to run this in docker, simply type the below commands [either use Option-A or Option-B]



## Option-A: using docker run command

***First download the env folder at your own localhost, then run the below commands where the env directory is present.***

Then run:

*docker network create goals-net*

**running mongodb:**

*docker run --name mongodb -v data:/data/db --rm -d --env-file ./env/mongo.env --network goals-net mongo*


**running backend:**

*docker pull mdabbasali/app-goals-backend:v2*

*docker run --name backend --rm -d --env-file ./env/backend.env --network goals-net mdabbasali/app-goals-backend:v2*


**running frontend:**

*docker pull mdabbasali/app-goals-frontend:v3*

*docker run --name my-app-frontend-goals-react --rm -d -p 3000:80 --network goals-net -it mdabbasali/app-goals-frontend:v3*



## Option-B: using docker-compose

***First download the env folder and docker-compose.yaml file to your own localhost, then run the below commands where the env directory and docker-compose.yaml are present.***

- docker-compose command must be installed in your host already.
  
run:

*docker-compose up -d*

**to stop:**

*docker-compose down*


Docker will then create the MongoDB from the stock mongo image. 
The backend-api uses nodejs and is built from a node:latest. 
The front end uses ReactJS and built from a node:14-alpine and then deployed under nginx. Check the Dockerfile under frontend.


# Note:
If you run those docker commands in your **Windows host** (if Docker is installed in Windows)

then you can browse the frontend app as 
  - http://localhost:3000

    or as by IP
  - http://<windows_host_IP>:3000

or
If you want to run those docker commands in a **remote Linux host** [where Docker is installed in Linux platform] (you access it via SSH from your Windows host) then 
Then, browse this address [in the Windows host (the host from where you are launching the SSH client)] 
  - http://<remote_linux_host_IP>:3000

Make sure that the port 3000 is allowed in your remote Linux host firewalld service.

*sudo firewall-cmd --add-port=3000/tcp --permanent*

*sudo firewall-cmd --reload*
