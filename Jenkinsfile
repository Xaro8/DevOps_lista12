pipeline {
    agent {
        docker {
            image 'python:3.11'
            args '-u root:root'
        }
    }

    stages {
        stage('Debug') {
            steps {
                sh 'python --version'
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
