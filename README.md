A demonstration of Docker Image build and running container to implement a simple 3 tier architecture.

frontend (React)

backend (nodejs REST API)

db (mongodb)



frontend will be able to access the mid-tier (backend)
The backend (mid-tier) will be able to access the db


In order to run this in docker, simply type 


running mongodb:

docker run --name my-mongo-db --rm -d --env-file ./env/mongo.env  -p 27017:27017 mongo


running backend:

docker pull mdabbasali/app-goals-backend:v2

docker run --name my-app-backend-goals --rm -d -p 80:80 --env-file ./env/backend.env \
--add-host=host.docker.internal:host-gateway mdabbasali/app-goals-backend:v2


running frontend:

docker pull mdabbasali/app-goals-frontend:v2

docker run --name my-app-frontend-goals-react --rm -d -p 3000:80 -it mdabbasali/app-goals-frontend:v2


Docker will then create the MongoDB from the stock mongo image. 
The backend-api uses nodejs with express and is built from a node:latest. 
The front end uses ReactJS and built from a node:14-alpine and then deployed under nginx. Check the Dockerfile under frontend.
