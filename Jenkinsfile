pipeline {
    agent docker-node-alpine

    environment {
        CI = 'true'
    }

    stages {
        stage('Test') {
            steps {
                sh 'sh ./jenkins/scripts/test.sh'
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
