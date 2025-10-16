pipeline {
    agent any

    environment {
        // IMPORTANT: Change this to your Docker Hub username and a chosen app name
        DOCKER_IMAGE = 'atharvn03/my-sample-app' 
        // This is the ID for the credentials you created in Jenkins
        REGISTRY_CREDENTIALS = 'dockerhub-credentials'
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out code...'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Docker image: ${DOCKER_IMAGE}:${env.BUILD_NUMBER}"
                    docker.build("${DOCKER_IMAGE}:${env.BUILD_NUMBER}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    echo "Pushing image to Docker Hub..."
                    docker.withRegistry('https://registry.hub.docker.com', REGISTRY_CREDENTIALS) {
                        docker.image("${DOCKER_IMAGE}:${env.BUILD_NUMBER}").push()
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy stage complete. Image is available on Docker Hub.'
            }
        }
    }
}
