pipeline {
    agent any
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver for development') {
            when {
                branch 'development' 
            }
            steps {
                script {
                    if (isUnix()) {
                        // For Unix-like systems
                        sh 'nohup ./jenkins/scripts/deliver-for-development.sh &'
                    } else {
                        // For Windows systems
                        bat 'start /b ./jenkins/scripts/deliver-for-development.bat'
                    }
                }
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'  
            }
            steps {
                script {
                    if (isUnix()) {
                        // For Unix-like systems
                        sh 'nohup ./jenkins/scripts/deploy-for-production.sh &'
                    } else {
                        // For Windows systems
                        bat 'start /b ./jenkins/scripts/deploy-for-production.bat'
                    }
                }
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
