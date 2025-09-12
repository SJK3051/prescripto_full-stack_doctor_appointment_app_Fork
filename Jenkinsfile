pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/naveenpudi/prescripto_full-stack_doctor_appointment_app_Fork.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    sh 'docker-compose build'
                }
            }
        }

        stage('Run Containers') {
            steps {
                script {
                    sh 'docker-compose up -d'
                }
            }
        }

        stage('Post-Deployment Check') {
            steps {
                script {
                    sh 'docker ps'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished!'
        }
    }
}
