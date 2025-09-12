

pipeline {
    agent {
        docker {
            image 'docker:24.0.2-dind'
            args '--privileged -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/naveenpudi/prescripto_full-stack_doctor_appointment_app_Fork.git'
            }
        }

        stage('Build & Deploy') {
            steps {
                sh 'apk add --no-cache docker-compose'  // install docker-compose in container
                sh 'docker-compose build'
                sh 'docker-compose down || true'
                sh 'docker-compose up -d'
            }
        }

        stage('Check Containers') {
            steps {
                sh 'docker ps -a'
            }
        }
    }
}
