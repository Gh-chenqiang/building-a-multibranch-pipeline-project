pipeline {
    agent {
        docker {
            image 'node:14.21.3-alpine'
            args '-p 3000:3000 -p 5000:5000'
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