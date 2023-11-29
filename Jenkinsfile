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
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'sh ./jenkins/scripts/test.sh'
            }
        }
    }
}
