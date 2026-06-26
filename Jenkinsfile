pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run App') {
            steps {
                sh '''
                    pm2 stop brain-task-app || true
                    pm2 start index.js --name brain-task-app
                '''
            }
        }

    }

    post {
        success {
            echo 'App deployed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs above.'
        }
    }
}

