pipeline {
    agent any

    // This tells Jenkins to check GitHub for new commits every minute
    triggers {
        pollSCM('* * * * *') 
    }

    environment {
        DOCKER_USER  = "manojgk1089"
        API_REPO     = "mean-api"
        WEB_REPO     = "mean-frontend"
        BUILD_TAG    = "build-${env.BUILD_NUMBER}"
        DOCKER_TOKEN = "dckr_pat_9nhGBjEHjUnlWdTzIcSwjNUFORw"
    }

    stages {
        stage('1. Git Clone') {
            steps {
                git branch: 'master', url: 'https://github.com/manojgk0210-hue/Manoj-G-K-crud-dd-task-mean-app.git'
            }
        }

        stage('2. Build Images') {
            steps {
                sh '''
                    docker build -t ${DOCKER_USER}/${API_REPO}:${BUILD_TAG} ./backend
                    docker build -t ${DOCKER_USER}/${WEB_REPO}:${BUILD_TAG} ./frontend
                '''
            }
        }

        stage('3. Login and Push') {
            steps {
                sh '''
                    echo "${DOCKER_TOKEN}" | docker login -u ${DOCKER_USER} --password-stdin

                    # Push versioned build
                    docker push ${DOCKER_USER}/${API_REPO}:${BUILD_TAG}
                    docker push ${DOCKER_USER}/${WEB_REPO}:${BUILD_TAG}
                    
                    # Update 'latest' tag
                    docker tag ${DOCKER_USER}/${API_REPO}:${BUILD_TAG} ${DOCKER_USER}/${API_REPO}:latest
                    docker tag ${DOCKER_USER}/${WEB_REPO}:${BUILD_TAG} ${DOCKER_USER}/${WEB_REPO}:latest
                    
                    docker push ${DOCKER_USER}/${API_REPO}:latest
                    docker push ${DOCKER_USER}/${WEB_REPO}:latest
                '''
            }
        }

        stage('4. Cleanup') {
            steps {
                sh "docker rmi ${DOCKER_USER}/${API_REPO}:${BUILD_TAG} ${DOCKER_USER}/${WEB_REPO}:${BUILD_TAG} || true"
            }
        }
    }

    post {
        success {
            echo "New commit detected and pushed as Build #${env.BUILD_NUMBER}"
        }
        always {
            sh 'docker logout'
        }
    }
}
