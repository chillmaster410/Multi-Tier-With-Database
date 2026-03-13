pipeline {
    agent {
        kubernetes {
            yaml '''
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: maven
    image: maven:3.9.6-eclipse-temurin-17
    command:
    - cat
    tty: true
'''
        }
    }

    stages {
        stage('Git_Checkout') {
            steps {
                // Fixed: Added credentialsId to the git step
                git branch: 'main', 
                    credentialsId: 'githubtoken', 
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

