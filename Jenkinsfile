pipeline {
    agent any 

    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhub-credentials' // Set your Docker Hub credentials ID
        DOCKER_IMAGE_NAME = 'sakheen555/Task3image' // Update with your Docker Hub username and image name
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from GitHub
                git url: 'https://github.com/sakheenmumtaz/MLOps_Task03.git', branch: 'main' // Update with your repo URL and branch
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh "docker build -t ${DOCKER_IMAGE_NAME}:latest ."
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
                        // Do nothing; this step authenticates
                    }
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Push the Docker image to Docker Hub
                    sh "docker push ${DOCKER_IMAGE_NAME}:latest"
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
