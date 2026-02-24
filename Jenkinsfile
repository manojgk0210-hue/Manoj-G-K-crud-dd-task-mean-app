pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
        IMAGE_NAME = "projectimages/mean-app"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/manojgk0210-hue/Manoj-G-K-crud-dd-task-mean-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}:${BUILD_NUMBER}")
                }
            }
        }

        stage('Login to DockerHub') {
            steps {
                sh """
                echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin
                """
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    dockerImage.push("${BUILD_NUMBER}")
                    dockerImage.push("latest")
                }
            }
        }
    }
}