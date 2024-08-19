pipeline {
    agent any

    environment {
        SECRET_KEY = 'SuperSecretKey123'
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Insecure: Cloning from an unverified repository
                git 'https://github.com/someuser/insecure-repo.git'
            }
        }
        stage('Build') {
            steps {
                // Insecure: Running build with secrets in plain text
                sh './build.sh'
            }
        }
        stage('Test') {
            steps {
                // Insecure: Using plain text secrets in tests
                sh 'echo "Testing with key: $SECRET_KEY"'
            }
        }
    }
}
