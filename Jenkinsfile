pipeline {
    agent any

    environment {
        IMAGE_NAME = "destino-project"
        CONTAINER_NAME = "destino-container"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/karthikjerryd/destino-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                script {
                    sh 'docker stop $CONTAINER_NAME || true'
                    sh 'docker rm $CONTAINER_NAME || true'
                }
            }
        }

        stage('Run New Container') {
            steps {
                sh '''
                docker run -d -p 80:80 \
                --name $CONTAINER_NAME \
                $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful 🚀'
        }
        failure {
            echo 'Deployment Failed ❌'
        }
    }
}