pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git credentialsId: 'github-token', url: 'https://github.com/YOUR_ID/YOUR_REPO.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t flask-app:latest .'
            }
        }
        stage('Deploy') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
                sh 'kubectl apply -f k8s/service.yaml'
            }
        }
    }
}
