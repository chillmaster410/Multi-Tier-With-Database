pipeline {
    agent any
    
    tools {
        maven 'TMaven'
        jdk 'java17'
    }
    parameters{
        string(name: 'Branch_name', defaultvalue: 'main', description:'GIT branch name to build')
    }

    stages {
        stage('Git_Checkout') {
            steps {
                // Fixed: Added credentialsId to the git step
                git branch: "${params.Branch_name}", 
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
    post {
        success {
            build job: 'start'
        }
    }
}




