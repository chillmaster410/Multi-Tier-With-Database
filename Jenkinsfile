pipeline {
    agent any
    
    tools {
        maven 'TMaven'
        jdk 'java17'
    }

    stages {
        stage('Git_Checkout') {
            steps {
                // Fixed: Added credentialsId to the git step
                git branch: 'main', 
                    credentialsId: 'github_access', 
                    url: 'https://github.com/chillmaster410/test-multi'
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
    
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
   
        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }          
    }
}

