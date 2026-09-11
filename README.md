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


8. Task 6 troubleshooting 


9.  Task 7 CICD Design 

Developer on git Push --> Source Repository( GITHUB) --> CI Pipeline (Github Actions)( RUN Test cases-> Run Linting Tests --> Run static Applicaiton Testing)