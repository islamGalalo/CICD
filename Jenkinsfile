pipeline {
    agent any

    environment {
        // Docker image name and Docker Hub credentials ID
        DOCKER_IMAGE = 'myapp'
        DOCKER_CREDENTIALS_ID = 'dckr_pat_PaGtvH1aHTCxczBoFitjb-Fh01g'  // Jenkins credentials for Docker Hub
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
                    sh 'docker build -t myapp .'
                }
            }
        }

       
        stage('Login to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub using Jenkins credentials
                    withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTIALS_ID}", usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    }
                }
            }
        }
    
        stage('Push Docker Image to Docker Hub') {
            steps {
                script {
                    // Tag and push the Docker image to Docker Hub
                    sh 'sudo docker tag caca1587355f domain.com/repo/tag_docker_name:latest'
                    sh 'sudo docker push galaldevops/depi_project:finalapp'
                }
            }
        }
    }

    post {
        success {
            // Send Slack notification on success
            sh """
            curl -X POST -H 'Content-type: application/json' --data '{
                "text": "Docker image ${DOCKER_REPO}:latest has been successfully pushed to Docker Hub."
            }' ${SLACK_WEBHOOK}
            """
        }
        failure {
            // Send Slack notification on failure
            sh """
            curl -X POST -H 'Content-type: application/json' --data '{
                "text": "Pipeline failed while building or pushing the Docker image."
            }' ${SLACK_WEBHOOK}
            """
        }
    }
}
