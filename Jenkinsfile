pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = 'react-app-docker'  // Set your Docker Hub repository here
        CONTAINER_NAME = 'react-container'
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the Git repository
                git branch: 'main', url: 'https://github.com/shamanthsham459/HelloWorld_React_Docker.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build the Docker image
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                // Stop any existing container
                script {
                    sh 'docker stop $CONTAINER_NAME || true'
                    sh 'docker rm $CONTAINER_NAME || true'
                    
                    // Run the new container
                    sh 'docker run -d --restart unless-stopped --name $CONTAINER_NAME -p 3000:80 $DOCKER_IMAGE'
                }
            }
        }
    }

    post {
        always {
            // Clean up the workspace after the build
            cleanWs()
        }
    }
}
