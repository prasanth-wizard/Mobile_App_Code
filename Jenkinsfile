pipeline {
    agent any

    environment {
        DOCKER_USER = "prasanth0003"
        IMAGE_NAME = "mobileapp"
        IMAGE_TAG = "1"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/prasanth-wizard/Mobile_App_Code.git'
            }
        }

        stage('Docker Build & Run') {
            steps {
                // Build Docker image with your Docker Hub username
                sh "docker build -t ${DOCKER_USER}/${IMAGE_NAME}:${IMAGE_TAG} ."
                
                // Stop and remove existing container if running
                sh "docker rm -f ${IMAGE_NAME} || true"
                
                // Run the container
                sh "docker run -d -p 8081:80 --name ${IMAGE_NAME} ${DOCKER_USER}/${IMAGE_NAME}:${IMAGE_TAG}"
            }
        }
    }

    post {
        success {
            echo "Docker container deployed successfully at http://localhost:8081"
        }
        failure {
            echo 'Build or deployment failed.'
        }
    }
}
