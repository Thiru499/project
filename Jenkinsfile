pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = 'react-app'
        DOCKERHUB_USERNAME = 'thiru876'
        DOCKERHUB_CREDENTIALS_ID = 'docker'
        DOCKER_REPO = 'prod'  // The name of the existing repository on Docker Hub
    }
    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/Thiru499/project.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image and tag it with 'prod' repository and 'prod' tag
                    docker.build("${DOCKERHUB_USERNAME}/${DOCKER_REPO}:${DOCKER_IMAGE_NAME}")
                }
            }
        }
        stage('Push to Docker Hub - Prod') {
            steps {
                script {
                    // Push the image to the existing 'dev' repository with the 'dev' tag
                    docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CREDENTIALS_ID) {
                        docker.image("${DOCKERHUB_USERNAME}/${DOCKER_REPO}:${DOCKER_IMAGE_NAME}").push("prod")	
                    }
                }
            }
        }
    }
    post {
        always {
            cleanWs()  // Clean workspace after each run
        }
    }
}
