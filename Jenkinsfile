
pipeline {
    agent any

    environment {
        REGISTRY = "your-dockerhub-username"
        APP_NAME = "your-app"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/your/repo.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    docker.build("${REGISTRY}/${APP_NAME}-admin", "./admin")
                    docker.build("${REGISTRY}/${APP_NAME}-backend", "./backend")
                    docker.build("${REGISTRY}/${APP_NAME}-frontend", "./frontend")
                }
            }
        }

        stage('Push Images') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    script {
                        docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-creds') {
                            docker.image("${REGISTRY}/${APP_NAME}-admin").push("latest")
                            docker.image("${REGISTRY}/${APP_NAME}-backend").push("latest")
                            docker.image("${REGISTRY}/${APP_NAME}-frontend").push("latest")
                        }
                    }
                }
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                sh 'docker-compose down'
                sh 'docker-compose up -d --build'
            }
        }
    }
}
