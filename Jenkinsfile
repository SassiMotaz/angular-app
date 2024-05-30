pipeline {
    agent any
    environment {
        DOCKER_IMAGE_FRONTEND = "docker-desktop/angular-app"
        DOCKER_IMAGE_BACKEND = "docker-desktop/springboot"
        DOCKER_TAG = "latest"
    }
    stages {
        stage('Build Angular') {
            steps {
                dir('angular-app') {
                    script {
                        sh 'docker build -t ${DOCKER_IMAGE_FRONTEND}:${DOCKER_TAG} .'
                    }
                }
            }
        }
        stage('Build Spring Boot') {
            steps {
                dir('springboot') {
                    script {
                        sh 'docker build -t ${DOCKER_IMAGE_BACKEND}:${DOCKER_TAG} .'
                    }
                }
            }
        }
        stage('Push Docker Images') {
            steps {
                script {
                        sh "docker push ${DOCKER_IMAGE_FRONTEND}:${DOCKER_TAG}"
                        sh "docker push ${DOCKER_IMAGE_BACKEND}:${DOCKER_TAG}"
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
