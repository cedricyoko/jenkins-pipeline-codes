pipeline {
    agent any

    environment {
        AWS_REGION = "us-east-1"
        ECR_REPO = "215925484801.dkr.ecr.us-east-1.amazonaws.com/jenkins-repo"
    }

    stages {
        stage('codescan') {
            steps {
                sh 'trivy fs . -o result.html'
            }
        }

        stage('dockerImageBuild') {
            steps {
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin $ECR_REPO'
                
                
                sh 'docker build -t jenkins-repo:latest .'
                sh 'docker build -t imageversion:latest .'
                sh 'docker tag jenkins-repo:latest $ECR_REPO:latest'
                sh 'docker tag imageversion:latest $ECR_REPO:v.$BUILD_NUMBER'
                sh 'docker push $ECR_REPO:latest'
                sh 'docker push $ECR_REPO:v.$BUILD_NUMBER'
            }
        }

        stage('checkcontainer') {
            steps {
                sh 'docker ps -a'
            }
        }
    }
}
