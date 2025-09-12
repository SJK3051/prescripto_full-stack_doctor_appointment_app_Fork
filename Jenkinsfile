pipeline {
    agent any

    environment {
        DOCKER_COMPOSE = "docker-compose"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://your-repo-url.git'
            }
        }

        stage('Build Images') {
            steps {
                script {
                    sh "${DOCKER_COMPOSE} build"
                }
            }
        }

        stage('Deploy Containers') {
            steps {
                script {
                    sh "${DOCKER_COMPOSE} down"
                    sh "${DOCKER_COMPOSE} up -d"
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                script {
                    sh 'docker ps -a'
                }
            }
        }
    }

    post {
        failure {
            echo "Deployment failed!"
        }
        success {
            echo "Deployment completed successfully ✅"
        }
    }
}

