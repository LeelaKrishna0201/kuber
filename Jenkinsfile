pipeline {
    agent any
    environment {
        IMAGE_NAME = "myapp:${BUILD_NUMBER}"
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/LeelaKrishna0201/kuber.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'eval $(minikube -p minikube docker-env) && docker build -t $IMAGE_NAME .'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig', variable: 'KUBECONFIG')]) {
                    sh 'kubectl apply -f deployment.yaml'
                }
            }
        }
    }
}
