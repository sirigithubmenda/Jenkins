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
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f serviceaccount.yaml'
            }
        }
        stage('Demo Scaling') {
            steps {
                // Perform scaling operations in Kubernetes
                sh 'kubectl scale deployment example-deployment --replicas=3'
            }
        }
    }
}     
