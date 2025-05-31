pipeline {
    agent any
    environment {
        IMAGE_NAME = "yourdockerhubusername/flaskapp"
        IMAGE_TAG = "latest"
    }
    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/yourusername/flask-docker-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', passwordVariable: 'DOCKER_PWD', usernameVariable: 'DOCKER_USER')]) {
                    sh 'echo $DOCKER_PWD | docker login -u $DOCKER_USER --password-stdin'
                    sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }

        stage('Deploy with Ansible') {
            steps {
                sh 'ansible-playbook -i inventory.yml deploy.yml'
            }
        }
    }
}
