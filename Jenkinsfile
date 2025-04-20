pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = 'react-app'
        DOCKERHUB_USERNAME = 'thiru876'
        DOCKERHUB_CREDENTIALS_ID = 'thiru8767'
        DOCKER_REPO = 'dev'  // The name of the existing repository on Docker Hub
    }
    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'dev', url: 'https://github.com/Thiru499/project.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image and tag it with 'dev' repository and 'dev' tag
                    docker.build("${DOCKERHUB_USERNAME}/${DOCKER_REPO}:${DOCKER_IMAGE_NAME}")
                }
            }
        }
        stage('Push to Docker Hub - Dev') {
            steps {
                script {
                    // Push the image to the existing 'dev' repository with the 'dev' tag
                    docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CREDENTIALS_ID) {
                        docker.image("${DOCKERHUB_USERNAME}/${DOCKER_REPO}:${DOCKER_IMAGE_NAME}").push("dev")	
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
