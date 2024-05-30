pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/SassiMotaz/angular-app.git'
            }
        }
        stage('Build Angular') {
            steps {
                dir('angular-app') {
                    script {
                        sh 'docker build -t frontend .'
                    }
                }
            }
        }
        stage('Build Spring Boot') {
            steps {
                dir('springboot') {
                    script {
                        sh 'docker build -t backend .'
                    }
                }
            }
        }
        stage('Push Docker Images') {
            steps {
                script {
                        sh "docker push your_dockerhub_username/angular-app:latest"
                        sh "docker push your_dockerhub_username/springboot:latest"
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh 'docker-compose down'
                    sh 'docker-compose up -d'
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
