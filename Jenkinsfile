pipeline {
    agent any

    environment {
        IMAGE_NAME = "flaskapp"
        IMAGE_TAG = "latest"
        CONTAINER_NAME = "flask-container"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/HareeshGullipalli/cicd-flask-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
            }
        }
        stage('Stop Old Container') {
            steps {
                sh "docker stop flask-container || true"
                sh "docker rm flask-container || true"
            }
        }
        

        stage('Run New Container') {
            steps {
                sh "docker run -d -p 80:5000 --name ${CONTAINER_NAME} ${IMAGE_NAME}:${IMAGE_TAG}"
            }
        }
    }
}
