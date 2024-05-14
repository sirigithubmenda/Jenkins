pipeline {
    agent any
    
    stages {
        stage('Checkout Source Code') {
            steps {
                // Checkout source code from your version control system
                checkout([$class: 'GitSCM', branches: [[name: '*/main/']], userRemoteConfigs: [[url: 'https://github.com/sirigithubmenda/Jenkins.git']]])
            }
        }
    }
}       
