pipeline {
    agent any

    stages {
        stage('codescan') {
            steps {
                sh 'trivy --version'
                
            }
        }
        stage('dockerversion') {
            steps {
                sh 'docker -v'
            }
        }
        stage('checkcontainer') {
            steps {
                sh 'docker ps -a'
                
            }
        }
    }
    
}