pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/SJK3051/prescripto_full-stack_doctor_appointment_app_Fork.git'
            }
        }

        stage('Build & Deploy') {
            steps {
                script {
                    // Stop running containers if any
                    sh 'docker-compose down'

                    // Build and start fresh containers
                    sh 'docker-compose up -d --build'
                }
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful!"
        }
        failure {
            echo "❌ Deployment failed!"
        }
    }
}

