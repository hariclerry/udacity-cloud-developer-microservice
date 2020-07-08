## Udagram microservice
Udagram is a simple cloud application developed alongside the Udacity Cloud Engineering Nanodegree. It allows users to register and log into a web client, post photos to the feed, and process photos using an image filtering microservice. Following are the services involved in this project:

* “user” - allows users to register and log into a web client, 
* “feed” - allows users to post photos, and process photos using image filtering 
* “frontend” - acts as an interface between the user and the backend-services
* "reverseproxy" - For resolving multiple services running on same port in separate containers

Correspondingly, the project is split into following parts:
1. The RestAPI Feed Backend, a Node-Express feed microservice.
2. The RestAPI User Backend, a Node-Express user microservice.
3. The Simple Frontend - A basic Ionic client web application which consumes the RestAPI Backend.
4. Nginx as a reverse-proxy server, when different backend services are running on the same port, then a reverse proxy server directs client requests to the appropriate backend server and retrieves resources on behalf of the client.  

### Dependencies
- Node/Express
- ionic
- AWS credentials and setup to connect to the postgres database

### Exercise Instructions
Follow the below instructions:
#### Instruction 1 - Clone the GitHub repo
1. Clone the following Git repository - https://github.com/hariclerry/udacity-cloud-developer-microservice
2. To run the application in a docker container, cd into course-03/exercises/udacity-c3-deployment/docker directory and follow the below steps;
    - Build docker images run `docker-compose -f docker-compose-build.yaml build --parallel`
    - To pull docker images from docker hub run `docker-compose -f docker-compose-build.yaml pull`
    - To start the container run `docker-compose up`
    - Navigate to the browser and run `http://localhost:8100` to see the Udagram application up and running 
    - To remove the container, run the following commands;
        `docker container ls
        docker container kill <container_name>
        docker container prune` 
 3. To run the application in a a kubernetes cluster, cd into course-03/exercises/udacity-c3-deployment/k8s directory and follow the below steps;
    - Run all deployments in the k8s, for example `kubectl apply -f reverseproxy-deployment.yaml`
    - Run all services in the k8s, for example `kubectl apply -f reverseproxy-service.yaml`
    - To start the backend services run `kubectl port-forward service/reverseproxy 8080:8080`
    - To start the frontend app run `kubectl port-forward service/frontend 8100:8100`
    - Navigate to the browser and run `http://localhost:8100` to see the Udagram application up and running 
    - To redeploy changes run `kubectl apply -f <name-deployment>.yaml` with the name of the deployment
    - To remove a deployment, run, for example `kubectl delete reverseproxy-deployment.yaml`
    - To remove a service, run, for example `kubectl delete svc reverseproxy`    