pipeline {
    agent any

    environment {
        // Docker image name and Docker Hub credentials ID
        DOCKER_IMAGE = 'myapp'
        DOCKER_CREDENTIALS_ID = 'jenkins2'  // Jenkins credentials for Docker Hub
        DOCKER_REPO = 'https://hub.docker.com/r/galaldevops/depi_project'  // Replace with your Docker Hub repository
     }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from Git
                git branch: 'main', url: 'https://github.com/islamGalalo/CICD.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh 'docker build -t galaldevops/myapp:latest .'
                }
            }
        }

       
        stage('Login to Docker Hub& push') {
            steps {
                script {
                    // Login to Docker Hub using Jenkins credentials
                    withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTIALS_ID}", usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                         sh 'docker push galaldevops/myapp:latest'
                    }
                }
            }
        }
    

   
}
}
