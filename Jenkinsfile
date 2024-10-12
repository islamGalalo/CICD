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



   
  
}

