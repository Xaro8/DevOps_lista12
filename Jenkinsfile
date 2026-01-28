pipeline {
    agent any

    stages {
        stage('Debug') {
            steps {
                sh 'python3 --version'
                sh 'pip --version'
            }
        }

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh 'pytest'
            }
        }
    }
}
