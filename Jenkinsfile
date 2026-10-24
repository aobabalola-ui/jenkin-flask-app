pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Getting application source code from GitHub'
                checkout scm
            }
        }

        stage('Verify Files') {
            steps {
                echo 'Checking project files'
                sh 'ls -la'
            }
        }

        stage('Test') {
            steps {
                echo 'Running Flask automated test'

                sh '''
                    python3 -m venv .venv
                    . .venv/bin/activate
                    pip install -r requirements.txt
                    pip install pytest
                    PYTHONPATH=. python -m pytest -v
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Flask Docker image'

                sh '''
                    docker build -t flask-app:${BUILD_NUMBER} .
                    docker tag flask-app:${BUILD_NUMBER} flask-app:latest
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying Flask application'

                sh '''
                    docker rm -f flask-test || true
                    docker rm -f flask-app || true

                    docker run -d \
                        --name flask-app \
                        -p 5000:5000 \
                        flask-app:${BUILD_NUMBER}
                '''
            }
        }
    }
}