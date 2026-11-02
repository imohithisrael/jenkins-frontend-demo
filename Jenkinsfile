
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
                sh 'docker build -t cicd-frontend:latest .'
            }
        }

        stage('Test Website') {
            steps {
                sh 'docker run --rm cicd-frontend:latest nginx -t'
            }
        }

        stage('Deploy Website') {
            steps {
                sh '''
                docker rm -f cicd-frontend || true
                docker run -d --name cicd-frontend -p 8081:80 cicd-frontend:latest
                '''
            }
        }
    }
}
