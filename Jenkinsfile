pipeline {
    agent any

    environment {
        AWS_REGION = "us-east-1"
        ECR_REPO = "801296747126.dkr.ecr.us-east-1.amazonaws.com"
    }

    stages {
        stage('codescan') {
            steps {
                sh 'trivy fs . -o result.html'
            }
        }

        stage('dockerImageBuild') {
            steps {
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 215925484801.dkr.ecr.us-east-1.amazonaws.com'
                
                
                sh 'docker build -t jenkins-repo .'
                sh 'docker tag jenkins-repo:latest 215925484801.dkr.ecr.us-east-1.amazonaws.com/jenkins-repo:latest'
                sh 'docker push 215925484801.dkr.ecr.us-east-1.amazonaws.com/jenkins-repo:latest'
            }
        }

        stage('checkcontainer') {
            steps {
                sh 'docker ps -a'
            }
        }
    }
}
