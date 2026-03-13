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
    
    parameters {
        string(name: 'Branch_name', defaultValue: 'main', description: 'GIT branch name to build')
    }

    stages {
        stage('Git_Checkout') {
            steps {
                // We do checkout in the default 'jnlp' agent container
                git branch: "${params.Branch_name}", 
                    credentialsId: 'githubtoken', 
                    url: 'https://github.com/chillmaster410/test-multi'
            }
        }

        stage('Compile') {
            steps {
                container('maven') {
                    sh 'mvn compile'
                }
            }
        }
    
        stage('Test') {
            steps {
                container('maven') {
                    sh 'mvn test'
                }
            }
        }
   
        stage('Package') {
            steps {
                container('maven') {
                    sh 'mvn package'
                }
            }
        }          
    }

    post {
        success {
            build job: 'start'
        }
    }
}
