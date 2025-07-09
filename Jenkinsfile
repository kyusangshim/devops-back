pipeline {
    agent any

    environment {
        IMAGE_NAME = "fast-api"
        CONTAINER_NAME = "fast-api-container"
        PORT = "8000"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $IMAGE_NAME ."
            }
        }

        stage('Deploy') {
            steps {
                sh "docker rm -f $CONTAINER_NAME || true"
                sh "docker run -d -p ${PORT}:80 --name $CONTAINER_NAME $IMAGE_NAME"
            }
        }
        

        stage('Check Running Container') {
            steps {
                echo "✅ 현재 실행 중인 컨테이너 목록:"
                sh "docker ps"
            }
        }
    }

    post {
        success {
            echo "✅ 배포 성공!"
        }
        failure {
            echo "❌ 배포 실패!"
        }
    }
}