pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
        DOCKERHUB_REPO = 'mukesh18s/nodejs'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Build the Docker image
                    def app = docker.build("${DOCKERHUB_REPO}:${env.BUILD_ID}")
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Run tests (optional)
                    def app = docker.image("${DOCKERHUB_REPO}:${env.BUILD_ID}")
                    app.inside {
                        sh 'npm install'
                        sh 'npm test'
                    }
                }
            }
        }

        stage('Push') {
            steps {
                script {
                    // Push the Docker image to Docker Hub
                    docker.withRegistry('https://registry.hub.docker.com', 'DOCKERHUB_CREDENTIALS') {
                        def app = docker.image("${DOCKERHUB_REPO}:${env.BUILD_ID}")
                        app.push()
                    }
                }
            }
        }
    }

    post {
        always {
            script {
                // Clean up the Docker images
                def app = docker.image("${DOCKERHUB_REPO}:${env.BUILD_ID}")
                app.remove()
            }
        }
    }
}

