pipeline {
    agent any
    
    stages {
        stage('Checkout Source Code') {
            steps {
                // Checkout source code from your version control system
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/sirigithubmenda/Jenkins.git']]])
            }
        }
        stage('Run Tests') {
            steps {
                // Run your test suite
                sh 'npm install' // Or any other test setup command
                sh 'npm test'    // Or any other test running command
            }
        }
        stage('Build Container') {
            steps {
                // Build your Docker container
                sh 'docker build -t siridocker-image .'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                // Deploy your container to Kubernetes
                withCredentials([usernamePassword(credentialsId: 'siri-kube', usernameVariable: 'KUBE_USER', passwordVariable: 'KUBE_PASSWORD')]) {
                    sh 'kubectl config set-cluster minikube --server=https://192.168.49.2:8443 --insecure-skip-tls-verify'
                    sh 'kubectl config set-credentials $KUBE_USER --token=$KUBE_PASSWORD'
                    sh 'kubectl config set-context siri-context --cluster=minikube --user=$KUBE_USER'
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
