pipeline {
    agent any
    tools {
        maven 'maven_3_9_6'
        jdk 'jdk_11'
        nodejs 'nodejs_14_17_0'
    }
    stages {
        stage('Clean up') {
            steps {
                deleteDir()
            }
        }
        stage('Clone repo') {
            steps {
                script {
                    // Clone the repository; use sh for Unix and bat for Windows
                    if (isUnix()) {
                        sh 'git clone https://github.com/SassiMotaz/angular-app.git'
                    } else {
                        bat 'git clone https://github.com/SassiMotaz/angular-app.git'
                    }
                }
            }
        }
        stage('Generate backend image') {
            steps {
                dir('angular-app') {
                    script {
                        // Use sh for Unix and bat for Windows
                        if (isUnix()) {
                            sh 'mvn clean install'
                            sh 'docker build -t backend .'
                        } else {
                            bat 'mvn clean install'
                            bat 'docker build -t backend .'
                        }
                    }
                }
            }
        }

        stage('Generate frontend image') {
            steps {
                dir('angular-app') {
                    script {
                        // Use sh for Unix and bat for Windows
                        if (isUnix()) {
                            sh 'npm install'
                            sh 'npm run build'
                            sh 'docker build -t frontend .'
                        } else {
                            bat 'npm install'
                            bat 'npm run build'
                            bat 'docker build -t frontend .'
                        }
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Use sh for Unix and bat for Windows
                    if (isUnix()) {
                        sh 'docker-compose up -d'
                    } else {
                        bat 'docker-compose up -d'
                    }
                }
            }
        }
    }
}