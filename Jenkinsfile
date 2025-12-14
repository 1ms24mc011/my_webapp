pipeline {
    agent any

    environment {
        IMAGE_NAME = "aravind2003/my_webapp"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/1ms24mc011/my_webapp'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:latest ."
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
                        sh "docker push ${IMAGE_NAME}:latest"
                    }
                }
            }
        }
    }

    post {
        success {
            echo "✅ Image pushed successfully: ${IMAGE_NAME}:latest"
        }
        failure {
            echo "❌ Pipeline failed"
        }
    }
}
