pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                sh "echo "Executando o comando Docker Build""
            }
        }
        stage('Push Docker Image') {
            steps {
                sh "echo "Executando o comando Docker push""
            }
        }
        stage('Deploy no Kubernetes') {
            steps {
                sh "echo "Executando o comando kubectl apply""
            }
        }
    }
}