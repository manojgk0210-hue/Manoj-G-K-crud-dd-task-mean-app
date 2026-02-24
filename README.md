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

MEAN Stack CRUD Application Deployment
This project consists of a full-stack CRUD (Create, Read, Update, Delete) application for managing tutorials. It is built using the MEAN stack and is fully containerized and automated via a Jenkins CI/CD pipeline.

Project Overview
The application manages a Tutorial collection with the following data structure:

ID

Title

Description

Published Status

Features
Create new tutorials.

Retrieve all tutorials or search by title.

Update existing tutorial details.

Delete individual tutorials or all tutorials at once.

Technical Stack
Frontend: Angular 15

Backend: Node.js and Express

Database: MongoDB

CI/CD: Jenkins

Containerization: Docker

Manual Local Setup
Backend (Node.js Server)
Navigate to the backend directory:
cd backend

Install dependencies:
npm install

Database Configuration:
Update your MongoDB credentials in app/config/db.config.js.

Start the server:
node server.js

Frontend (Angular Client)
Navigate to the frontend directory:
cd frontend

Install dependencies:
npm install

Service Configuration:
Modify src/app/services/tutorial.service.ts to adjust the API base URL if necessary.

Start the client:
ng serve --port 8081

Access the application:
Open your browser and navigate to http://localhost:8081/

DevOps and Automation
Dockerization
The application is split into two main Docker images:

Backend API: manojgk1089/mean-api

Frontend Web: manojgk1089/mean-frontend

Jenkins CI/CD Pipeline
The included Jenkinsfile automates the following workflow:

Source Control: Automatically detects changes (commits) on the GitHub master branch.

Versioning: Tags every new build with a unique version number (e.g., build-42) using the ${env.BUILD_NUMBER} variable.

Authentication: Securely logs into Docker Hub using a Personal Access Token.

Build & Push: Builds both Docker images and pushes them to the Docker Hub registry.

Latest Tagging: Always updates the latest tag to point to the most recent successful build.

Cleanup: Removes local Docker images from the Jenkins agent to optimize disk space.

Important Commands
Docker Compose (Build and Run)
To run the entire stack (Database, Backend, and Frontend) with one command:
docker-compose up --build -d

Docker Manual Push (Example)
To manually tag and push an image (replace [BUILD_NO] with your version):
docker tag mean-api:latest manojgk1089/mean-api:[BUILD_NO]
docker push manojgk1089/mean-api:[BUILD_NO]

Checking Logs
To check the logs of the running backend container:
docker logs [container_id_or_name]

Environment Notes
Jenkins Credentials: Ensure you have a credential ID dockerhub-creds configured in Jenkins or use the environment variable method for the Docker Hub Token.

Port Mapping: The frontend is configured to run on port 8081. Ensure this port is open in your security groups or firewall.

Run `ng serve --port 8081`

You can modify the `src/app/services/tutorial.service.ts` file to adjust how the frontend interacts with the backend.

Navigate to `http://localhost:8081/`
