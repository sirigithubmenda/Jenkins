pipeline {
    agent any
    
    stages {
        stage('Checkout Source Code') {
            steps {
                // Checkout source code from your version control system
                git https://github.com/sirigithubmenda/Jenkins.git
            }
        }
        
        stage('Run Tests') {
            steps {
                // Run your tests here
                sh 'npm install' // Example command for installing dependencies
                sh 'npm test'    // Example command for running tests
            }
        }
        
        stage('Build Docker Container') {
            steps {
                // Build your Docker container
                sh 'docker build -t siridocker-image .'
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                // Deploy your container to Kubernetes
                withCredentials([usernamePassword(credentialsId: 'siri-jenkins', usernameVariable: 'KUBE_USER', passwordVariable: 'KUBE_PASSWORD')]) {
                    sh 'kubectl config set-cluster sirik8cluster.ap-northeast-1.eksctl.io --server=https://13BD250461E8A4BC131F9893C439DC3A.gr7.ap-northeast-1.eks.amazonaws.com --insecure-skip-tls-verify'
                    sh 'kubectl config set-credentials $KUBE_USER --token=$KUBE_PASSWORD'
                    sh 'kubectl config set-context siri-context --cluster=sirik8cluster.ap-northeast-1.eksctl.io --user=$KUBE_USER'
                    sh 'kubectl config use-context siri-context'
                    sh 'kubectl apply -f deployment.yaml'
                }
            }
        }
        
        stage('Demo Scaling') {
            steps {
                // Perform scaling operations in Kubernetes
                sh 'kubectl scale deployment jenkins --replicas=3'
            }
        }
    }
}

