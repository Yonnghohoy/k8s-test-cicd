pipeline {
    agent {
        kubernetes {
            label 'docker-agent'
            defaultContainer 'docker' // <== 여기 중요!
        }
    }
    stages {
        stage('Clone') {
            steps {
                git credentialsId: 'github-token', url: 'https://github.com/yonnghohoy/k8s-test-cicd.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                container('docker') {
                    sh 'docker version' // 컨테이너 안에서 docker 명령어 실행
                    sh 'docker build -t flask-app:latest .'
                }
            }
        }
        stage('Deploy') {
            steps {
                container('docker') {
                    sh 'kubectl apply -f k8s.yaml'
                }
            }
        }
    }
}
