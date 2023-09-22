## A demonstration of Docker Image build and running container to implement a simple 3 tier architecture.

- frontend (React)

- backend (nodejs REST API)

- db (mongodb)

ck

frontend will be able to access the mid-tier (backend)
The backend (mid-tier) will be able to access the db


#### In order to run this in docker, simply type the below commands [either use Option-A or Option-B]



## Option-A: using docker run command

***First download the env folder at your own localhost, then run the below commands where the env directory is present.***

Then run:

*docker network create goals-net*

**running mongodb:**

*docker run --name mongodb --rm -d --env-file ./env/mongo.env --network goals-net mongo*


**running backend:**

*docker pull mdabbasali/app-goals-backend:v2*

*docker run --name my-app-backend-goals --rm -d -p 80:80 --env-file ./env/backend.env --network goals-net mdabbasali/app-goals-backend:v2*


**running frontend:**

*docker pull mdabbasali/app-goals-frontend:v2*

*docker run --name my-app-frontend-goals-react --rm -d -p 3000:80 -it mdabbasali/app-goals-frontend:v2*



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
If you run those docker commands in your **Windows host**

then you can browse the frontend app as http://localhost:3000

or
If you want to run those docker commands in a **remote Linux host** (access via SSH) then 

  - firefox has to be already installed in that remote Linux host (if not then to install run: *yum install -y firefox*)
  
  - If X11 forwarding is already enabled in your remote Linux host then you need to export the display to your Windows host. To do that run this command (in the remote Linux host) $ *export DISPLAY=Windows_Host_IP:0.0* 
  
  - $ *firefox*  (run this command in the remote Linux host), It should pop up Firefox browser on your Windows host. 
   
  - Then, browse this address in Firefox (already popped up in the Windows host from where you are launching the SSH client) http://localhost:3000 
