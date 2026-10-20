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
                    pip install -r requirement.txt
                    pip install pytest
                    pytest -v
                '''
            }
        }
    }
}