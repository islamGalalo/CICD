pipeline {
    agent any

    environment {
        // Define the Docker image name
        DOCKER_IMAGE = 'myapp'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from version control (Git)
                git branch: 'main', url: 'https://github.com/islamGalalo/CICD.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image using the Dockerfile in the repo
                    sh 'docker build -t myapp .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run the Docker container and map ports
                    sh 'docker run -d --name finalproject -p 8080:80 myapp'
                }
            }
        }

        stage('Clean Up') {
            steps {
                script {
                    // Optional: Clean up old Docker images to free up space
                    sh 'docker rmi $(docker images -f "dangling=true" -q) || true'
                }
            }
        }
    }

    post {
        always {
            script {
                // Stop and remove the Docker container after the pipeline run
                sh 'docker stop myapp || true'
                sh 'docker rm myapp || true'
            }
        }
    }
}

