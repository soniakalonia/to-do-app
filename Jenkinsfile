pipeline {
    agent any

    environment {
        // Force Jenkins to use system Node (v20.12.2)
        PATH = "C:\\Program Files\\nodejs;${env.PATH}"
        FRONTEND_DIR = "client"
        BACKEND_DIR = "server"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/soniakalonia/to-do-app.git'
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
            bat 'set CI=false && npm run build'
        }
    }
}

        stage('Start Backend Server') {
            steps {
                dir("${BACKEND_DIR}") {
                    bat 'start /B npm start'
                }
            }
        }

        stage('Serve React Build on Port 3000') {
            steps {
                dir("${FRONTEND_DIR}") {
                    bat 'npx serve -s build -l 3000'
                }
            }
        }
    }

    post {
        success {
            echo 'APP DEPLOYED SUCCESSFULLY'
            echo 'Frontend: http://localhost:3000'
            echo 'Backend:  http://localhost:5000'
        }
        failure {
            echo 'PIPELINE FAILED'
        }
    }
}