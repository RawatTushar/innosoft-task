5. Task 3 Container Networking 


Q1. The application Connects to PostgresSQL using Docker COmpose internal Network And The PostgresSQL service name as the hostname .

Q2. To Prevent direct External Access to the database. Only the Application needs to communicate with PostgresSQL

Q3. Docker Compose Creates a shared network where services can communicate using their service names as DNS hostnames.

Q4. we have used "db" name 

Q5.  The applicaiton may temporarliy fail db operations while postgress is not available. Once its back the applciaiton can reconnect, depending on the application database connection/retry config.


7. Task 5 Data Persistance 


Q1. we created db_data, mounted to /var/lib/postgresql/data

Q2. becuase PostgreSQL data must survive even when the containers is killed,recreated, deleted or  restarted.

Q3. Db Containers stored data is lost. With db_data, the data remains and is available to the new PostgreSql Container.


8. Task 6 troubleshooting the 502 bad gateway

: Check all Containers 
  docker compose ps

: Check application logs 
  docker compose logs app_name
 
: Check Nginx logs 
  docker compose logs nginx

: check the Nginx Configurations 

: check the communication from Nginx-App
docker compose ps
docker compose exec nginx curl http://app:8080

:Check Docker Networks 
docker network ls 
docker network inspect <network_name>

: check app commmunication with Postgress
docker compose exec app curl http://db:5432

: test from your host 
curl http://localhost

9.  Task 7 CICD Design 

Developer on git Push --> Source Repository( GITHUB) --> CI Pipeline (Github Actions)( RUN Test cases-> Run Linting Tests --> Run static Applicaiton Testing) --> Build Docker Image --> Push Image To Image REpo ( Docker HUB or AWS ECR) --> Deployment (Using pull the images here and run docker compose )


Q1. I would  use Github ACtions for CICD Pipeline and deploying the image as it easier to implement and is ready to go with github.

Q2. We Can Store Docker Images inside any Image Registry such AS Docker Hub or AWS ECR .

Q3. Deployment could pulls the new image from the Container Registry we will use immutable git commit sha-25 as tag for our image too. 

Q4. We could perform a deployment with minimal or zero downtime using blue green Deployment or Rolling deployment. in case of Rolling deployment we could rollout our applicaiton one by one and as they are healthy we can slowly route the traffic to them and repeat the process untill all the containers are healthy and up then we can just destroy the old version.

Q5. Application/ Database credentials could be managed with .env file created on the server and we can also use AWS KMS Encryption for sensitive data or we can either use external secrets service such AWS Secrets Manager.

Q6. I would first investigate the LOGS and Metrics so as to check whether the issue is impacting the users massively.
then Would check the Deployment history to see whether there has been any recent deployments as of now 
if The deployment seems to be faulty i would rollback to previous Stable Deployment 
if not i WOuld Go and investigate my Containers health, status and server health , cpu usage .
if needed and the traffic is genuine i would add more instances to it or increase the resources .
if still didnt got the issue i would check new dependency from the development side and check its compatibilty. 

11. Readme prerequisites.

 ## Prerequisites
 install Docker and Docker Desktop on your System
 Setup Docker HUB 
 Docker Compose  

 ## Setup 
 Clone The Repository and move into the Project Directory.

 docker compose build
 docker compose up -d
 access the application at http://localhost

 Requested will flow like this :
 Client-> Nginx -> Nodejs -> PostgresQL

 ## Debug or Check 
 docker ps
 docker compose logs nginx
 curl http://localhost
 docker images 