# Overview
This project consists of two Golang microservices: one for managing user data and another for handling API methods. 
The services communicate over gRPC, utilize PostgreSQL and Redis for persistent and cached storage, and are containerized and deployed on Kubernetes.

## Prerequisites
1. Go (Golang) - [Install GO](https://go.dev/doc/install)
2. PostgreSQL - Install PostgreSQL
3. Redis - Install Redis
4. Docker - Install Docker.
5. Kubernetes - Use Minikube or another provider.
6. kubectl - Install kubectl.

## Golang Application
### Microservice 1 - User Management
**Provides the following functionalities:**
- Create User: Accepts user details and stores them in PostgreSQL, then caches in Redis.
- Get User by ID: Checks Redis for the user; if not present, fetches from PostgreSQL, caches the result.
- Update User: Updates the user's details in both PostgreSQL and Redis if cached.
- Delete User: Deletes the user from PostgreSQL and removes the cached data in Redis.

### Microservice 2 - API Service
**Functions**
- Method 1 (Sequential): Processes requests sequentially. Fetches users from PostgreSQL, waits as specified.
- Method 2 (Parallel): Processes requests in parallel. Fetches users from PostgreSQL, waits as specified.
- CRUD Operations: All CRUD operations route through the API gateway to the user service via gRPC.

### gRPC Communication
The two microservices communicate through gRPC for efficient data handling.

# Setup and Installation
1. Clone the repositories:

   ```bash
   https://github.com/shivarajshanthaiah/user-management-APIGateway/tree/5ee057f1a9429b3c6e558192b78f83c9398272dc
   https://github.com/shivarajshanthaiah/user-management-users/tree/24863428e39a2631e2edda12a61f4a018780ec07
2. Make sure to install gRPC(Protobuf) and database(PostgreSQL and Redis)
3. Set environmen variables
4. Make sure your services are up and running
5. Test API endpoints(refer [API documentation](https://documenter.getpostman.com/view/32823353/2sAY4ydzzB)

## Docker Containerization
You can either:
1. Clone the repository and Dockerize your application (refer to the [Docker 101 tutorial](https://www.docker.com/101-tutorial/) if you’re new to Docker), or
2. Pull Docker images directly from Docker Hub:
   ```bash
   docker pull shivaraj3652/user-management-apiservice:v1
   docker pull shivaraj3652/user-management-user:v1
3. Set Up PostgreSQL and Redis Containers:
Pull PostgreSQL and Redis images, set up the database, and connect both microservices.

#### Testing Locally with Docker
Ensure the application works as expected in Docker before deploying to Kubernetes.

## Kubernetes Deployment
For Kubernetes setup, you can refer to the [Kubernetes documentation](https://kubernetes.io/docs/tutorials/).
### Deployment Process
1. Create a Secret File (for database credentials and other sensitive information).
2. Clone Kubernetes Deployment Files (deployment.yaml and service.yaml).
3. Deploy the files to your Kubernetes cluster:
   ```bash
   kubectl apply -f deployment.yaml
   kubectl apply -f service.yaml

## Testing the Application
1. Get Service Details:
   ```bash
   kubectl get svc
2. Access Services via NodePort:
   ```bash
   http://<NodeIP>:<NodePort>/method

## Conclusion
This deployment demonstrates a basic Golang microservices setup with Docker and Kubernetes, using gRPC for communication, 
containerized deployments, and NodePort for external access testing.
