pipeline {
    agent any
    
    stages {
        stage('Checkout Source Code') {
            steps {
                // Checkout source code from your version control system
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[url: 'https://github.com/sirigithubmenda/Jenkins.git']]])
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
    }
}       
