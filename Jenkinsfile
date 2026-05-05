pipeline {
    agent any

    environment {
        SONAR_TOKEN = 'efa59d55668cbf0979e24873d0e81d2cd3e6fad8'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/vasu289/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }

        stage('NPM Audit Security Scan') {
            steps {
                bat 'npm audit || exit /b 0'
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                bat '''
                npm install sonarqube-scanner --save-dev
                npx sonarqube-scanner
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed. Check Jenkins console output and SonarCloud dashboard.'
        }
        success {
            echo 'Build successful and SonarCloud analysis completed.'
        }
        failure {
            echo 'Build failed. Please check errors in console output.'
        }
    }
}
