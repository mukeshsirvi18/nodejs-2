pipeline {
    agent any

    environment {
        DOCKER_HUB_REPO = 'mukesh18s/nodejs'
        DOCKER_HUB_CREDENTIALS = 'dockerhub_credentials'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${env.DOCKER_HUB_REPO}:latest")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('', "${env.DOCKER_HUB_CREDENTIALS}") {
                        docker.image("${env.DOCKER_HUB_REPO}:latest").push()
                    }
                }
            }
        }
    }
}


