pipeline {
    agent any
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'npm install'
                    } else {
                        bat 'npm install'
                    }
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    if (isUnix()) {
                        sh './jenkins/scripts/test.sh'
                    } else {
                        // Corrected path for Windows
                        bat '.\\jenkins\\scripts\\test.bat'
                    }
                }
            }
        }
    }
}
