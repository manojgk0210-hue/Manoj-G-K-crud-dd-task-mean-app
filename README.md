In this DevOps task, you need to build and deploy a full-stack CRUD application using the MEAN stack (MongoDB, Express, Angular 15, and Node.js). The backend will be developed with Node.js and Express to provide REST APIs, connecting to a MongoDB database. The frontend will be an Angular application utilizing HTTPClient for communication.  

The application will manage a collection of tutorials, where each tutorial includes an ID, title, description, and published status. Users will be able to create, retrieve, update, and delete tutorials. Additionally, a search box will allow users to find tutorials by title.

## Project setup

### Node.js Server

cd backend

npm install

You can update the MongoDB credentials by modifying the `db.config.js` file located in `app/config/`.

Run `node server.js`

### Angular Client

cd frontend

npm install
MEAN Stack CRUD Application with Docker and Jenkins
Introduction

This project is a full-stack CRUD application built using the MEAN stack (MongoDB, Express, Angular, Node.js). The application is fully containerized using Docker and managed using Docker Compose. A Jenkins pipeline is included to automate Docker image building and container deployment.

This project demonstrates practical DevOps concepts such as containerization, multi-container orchestration, and CI automation.

Project Architecture

The application consists of three main services:

Frontend: Angular application

Backend: Node.js and Express REST API

Database: MongoDB

The frontend communicates with the backend API, and the backend connects to MongoDB for data storage.

All services run inside separate Docker containers.

Technologies Used

Node.js

Express.js

Angular

MongoDB

Docker

Docker Compose

Jenkins

Git

Project Structure
project-root/
│
├── api/                    # Backend source code
│   ├── Dockerfile
│   └── package.json
│
├── web/                    # Frontend source code
│   ├── Dockerfile
│   └── package.json
│
├── docker-compose.yml      # Docker Compose configuration
├── Jenkinsfile             # Jenkins CI pipeline
└── README.md
Prerequisites

Make sure the following tools are installed on your system:

Docker

Docker Compose

Git

Jenkins (if running CI pipeline)

To verify Docker installation:

docker --version
docker compose version
Running the Application Using Docker Compose

Navigate to the root directory of the project where the docker-compose.yml file is located.

Build and start all services
docker compose up -d --build

This command will:

Build Docker images

Create containers

Start all services in detached mode

Stop all services
docker compose down
Stop and remove volumes (this deletes database data)
docker compose down -v
Application Access

After running Docker Compose, the application will be available at:

Frontend:

http://localhost:8081

Backend API:

http://localhost:8080

MongoDB:

Port 27017

If running on a cloud server (for example EC2), make sure required ports are open in the security group.

Building Docker Images Manually

If you want to build images without Docker Compose:

Build backend image
docker build -t mean-app-api ./api
Build frontend image
docker build -t mean-app-web ./web
Running Containers Manually
Run MongoDB
docker run -d -p 27017:27017 --name mongodb mongo
Run backend container
docker run -d -p 8080:8080 --name api mean-app-api
Run frontend container
docker run -d -p 8081:80 --name web mean-app-web
Jenkins CI Pipeline

This project includes a Jenkins pipeline that automates Docker image building and container execution.

The pipeline performs the following steps:

Removes any existing container

Builds a new Docker image

Tags the image using the Jenkins build number

Runs the container
