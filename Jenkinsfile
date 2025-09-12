pipeline {
    agent any

    environment {
        DOCKER_COMPOSE = "docker-compose"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: ''https://github.com/naveenpudi/prescripto_full-stack_doctor_appointment_app_Fork.git
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

