pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t destino-app .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop destino-container || true'
                sh 'docker rm destino-container || true'
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d -p 80:80 --name destino-container destino-app'
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful ✅'
        }
        failure {
            echo 'Deployment Failed ❌'
        }
    }
}