
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
    }
}