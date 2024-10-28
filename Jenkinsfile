pipeline {
    agent any
    environment {
        USER_REPO = "https://github.com/talanw/pipelines.git"
        USER_DIR = "${env.JENKINS_HOME}/user-${env.BUILD_NUMBER}"
    }
    stages {
        stage('Clone Repository') {
            steps {
                script {
                    // Clone repository into user-specific directory
                    sh "git clone ${USER_REPO} ${USER_DIR}"
                    dir("${USER_DIR}") {
                        // Security Issue: Hardcoded sensitive information
                        // Example of a make command that could expose sensitive data
                        sh 'make all'
                    }
                }
            }
        }
        // Additional stages can be added here
    }
    post {
        success {
            script {
                // Decrypt flag stored in Jenkins credentials
                sh "echo ${ENCRYPTED_FLAG} | base64 --decode > flag.txt"
                archiveArtifacts artifacts: 'flag.txt', fingerprint: true
            }
        }
    }
}