pipeline {
    agent any

    environment {
        // Name for your built image
        IMAGE_NAME = "my-nginx-app"
    }

    stages {
        stage('Fetch Source Code') {
            steps {
                // This builds on what Image 2 did to fetch your code
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Builds the Nginx Dockerfile we looked at earlier
                    sh "docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} ."
                }
            }
        }

        stage('Deploy Container') {
            steps {
                script {
                    // Stops any existing container running on port 80 to prevent conflicts
                    sh "docker rm -f my-running-nginx-app || true"
                    // Runs your newly built container
                    sh "docker run -d --name my-running-nginx-app -p 80:80 ${IMAGE_NAME}:${BUILD_NUMBER}"
                }
            }
        }
    }
}
