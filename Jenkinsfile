pipeline {
    agent any

    environment {
        NODEJS_HOME = "C:\\Program Files\\nodejs"
        PATH = "${NODEJS_HOME};${env.PATH}"
        FRONTEND_DIR = "client"
        BACKEND_DIR = "server"
        CI = "false"
        PORT = "3000"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/soniakalonia/to-do-app.git'
            }
        }

        stage('Check Node Version') {
            steps {
                bat 'node -v'
                bat 'npm -v'
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                dir("${BACKEND_DIR}") {
                    bat 'npm install'
                }
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                dir("${FRONTEND_DIR}") {
                    bat 'npm install'
                }
            }
        }

        stage('Build React App') {
            steps {
                dir("${FRONTEND_DIR}") {
                    bat 'npm run build'
                }
            }
        }

        stage('Start Backend Server') {
            steps {
                dir("${BACKEND_DIR}") {
                    bat 'start cmd /k npm start'
                }
            }
        }

        stage('Serve React Build on Port 3000') {
            steps {
                dir("${FRONTEND_DIR}") {
                    bat 'npm install -g serve'
                    bat 'start cmd /k serve -s build -l 3000'
                }
            }
        }
    }

    post {
        success {
            echo '🎉 PIPELINE SUCCESS — APP RUNNING ON http://localhost:3000'
        }
        failure {
            echo '❌ PIPELINE FAILED'
        }
    }
}