pipeline {
    agent {
        docker {
            image 'node:18.18.2-alpine'
            args '-p 3001:3001 -p 5001:5001'
        }
    }

    environment {
        CI = 'true'
    }

    stages {
        stage('Test') {
            steps {
                sh 'npm install'
            }
        }

        stage('Deliver for development') {
            when {
                branch 'development'
            }
            steps {
                sh 'sh ./jenkins/scripts/deliver-for-development.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh 'sh ./jenkins/scripts/kill.sh'
            }
        }

        stage('Deploy for production') {
            when {
                branch 'production'
            }
            steps {
                sh 'sh ./jenkins/scripts/dploy for production.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh 'sh ./jenkins/scripts/kill.sh'
            }
        }
    }
}