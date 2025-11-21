# User Registration App

A Spring Boot application for user registration, using MySQL as the database. The app is containerized with Docker and orchestrated using Docker Compose.

## Features
- User registration and management
- RESTful API endpoints
- MySQL database integration
- Docker and Docker Compose support

## Prerequisites
- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/)
- [Java 17+](https://adoptopenjdk.net/) (for local development)
- [Maven](https://maven.apache.org/) (for local development)

## Setup Instructions

### 1. Build the Application (Optional, for local development)
```
./mvn clean package
```
Or, if you are on Windows:
```
mvnw.cmd clean package
```

### 2. Build and Tag the Docker Image
```
docker build -t suneelseelam33/userregister-app:v1 .
```

### 3. Push the Image to Docker Hub
```
docker login
# After successful login:
docker push suneelseelam33/userregister-app:v1
```

### 4. Start the Application with Docker Compose
```
docker-compose up
```
This will start both the MySQL database and two instances of the application (on ports 8080 and 8081).

## API Usage Examples

### GET All Users
- App1:
  ```bash
  curl -X GET http://localhost:8080/users
  ```
- App2:
  ```bash
  curl -X GET http://localhost:8081/users
  ```

### POST Create User
- App1:
  ```bash
  curl -X POST http://localhost:8080/users \
    -H "Content-Type: application/json" \
    -d '{"name": "Alice", "email": "alice@example.com"}'
  ```
- App2:
  ```bash
  curl -X POST http://localhost:8081/users \
    -H "Content-Type: application/json" \
    -d '{"name": "Bob", "email": "bob@example.com"}'
  ```

#### More Example POST Calls to Populate Data
```bash
curl -X POST http://localhost:8080/users \
  -H "Content-Type: application/json" \
  -d '{"name": "Charlie", "email": "charlie@example.com"}'

curl -X POST http://localhost:8080/users \
  -H "Content-Type: application/json" \
  -d '{"name": "Diana", "email": "diana@example.com"}'
```

## Useful Links
- [Docker Hub Repository](https://hub.docker.com/repository/docker/suneelseelam33/userregister-app)
- [GitHub Repository](https://github.com/seelamsnl/userregister-app)

---

Feel free to contribute or raise issues!
