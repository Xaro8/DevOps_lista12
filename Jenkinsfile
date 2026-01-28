pipeline {
    agent any

    stages {
        stage('Debug') {
            steps {
                sh 'python3 --version'
                sh 'pip --version'
                sh 'python3 -m venv --help'
            }
        }

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install dependencies') {
            steps {
                sh '''
                     #!/bin/bash
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    #!/bin/bash
                    . venv/bin/activate
                    pytest
                '''
            }
        }
    }
}
