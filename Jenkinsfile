pipeline {
    agent any

    environment {
        SECRET_KEY = 'SuperSecretKey123'
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Cloning this repository (intentionally insecure)
                git 'https://github.com/YourUsername/Pipelines.git'
            }
        }
        stage('Build') {
            steps {
                sh './build.sh'
            }
        }
        stage('Test') {
            steps {
                sh 'echo "Testing with key: $SECRET_KEY"'
            }
        }
        stage('Security Check') {
            steps {
                script {
                    // Security check to ensure fixes have been applied
                    def secretCheck = sh(script: 'grep "SuperSecretKey123" secrets.sh', returnStatus: true)
                    def repoCheck = sh(script: 'grep "YourUsername/Pipelines.git" Jenkinsfile', returnStatus: true)
                    
                    if (secretCheck == 0 || repoCheck == 0) {
                        error "Security flaws still present. Fix them to proceed."
                    }
                }
            }
        }
        stage('Success') {
            steps {
                sh 'cat flag.txt'
            }
        }
    }
}
