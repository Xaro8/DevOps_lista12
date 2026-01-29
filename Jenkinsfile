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
        
        stage('Package application') {
            steps {
                sh '''
                mkdir -p dist
                tar -czf dist/app.tar.gz app.py requirements.txt
                '''
            }
        }

        stage('Upload to miniserve') {
            steps {
                sh '''
                curl -F "path=@dist/app.tar.gz" http://localhost:8888/upload?path=/uploads/
                '''
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'dist/app.tar.gz'
        }
    }
}
