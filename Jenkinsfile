pipeline {
    agent any

    environment {
        // Updated to match your repo name 'a'
        DOCKER_IMAGE = "sreevathsa221/a.py"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // This builds the image locally
                    docker.build("${DOCKER_IMAGE}:latest")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    // 'dockerhub-creds' must match the ID in Jenkins Manage Credentials
                    // This command handles the login AND the push automatically
                    docker.withRegistry('', 'dockerhub-creds') {
                        docker.image("${DOCKER_IMAGE}:latest").push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Image successfully built and pushed to Docker Hub'
        }
        failure {
            echo 'Pipeline failed - check the Console Output for errors'
        }
    }
}
