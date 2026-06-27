pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t brain-task-app .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop brain-task-app || true
                docker rm brain-task-app || true
                docker run -d --name brain-task-app -p 82:80 brain-task-app
                '''
            }
        }
    }

    post {
        success {
            echo 'Application deployed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}

