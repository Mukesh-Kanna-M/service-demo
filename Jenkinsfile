pipeline {
    agent any

    environment {
        IMAGE = "service:v3"
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/Mukesh-Kanna-M/service-demo.git'
            }
        }

        stage('Build Image') {
            steps {
                sh '''
                eval $(minikube docker-env)
                docker build -t $IMAGE .
                '''
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                kubectl apply -f deployment.yaml
                kubectl apply -f service.yaml
                '''
            }
        }

        stage('Verify') {
            steps {
                sh '''
                kubectl get pods
                kubectl get svc
                '''
            }
        }
    }
}
