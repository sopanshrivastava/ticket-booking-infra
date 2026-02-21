pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Create Namespace') {
            steps {
                sh '''
                kubectl get namespace infra || kubectl create namespace infra
                '''
            }
        }

        stage('Deploy Secrets') {
            steps {
                sh '''
                kubectl apply -n infra -f secrets/
                '''
            }
        }

        stage('Deploy Infra Components') {
            steps {
                sh '''
                kubectl apply -n infra -f base/
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                echo "Pods in infra namespace:"
                kubectl get pods -n infra
                '''
            }
        }
    }
}