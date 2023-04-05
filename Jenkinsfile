pipeline {
    agent any
    stages {
        stage('Create EKS Cluster') {
            steps {
                sh 'aws cloudformation create-stack --stack-name ronyEKS --template-body file://eks.yaml --region "us-east-1"' 
            }
        }
        stage('Create Node Group') {
            steps {
                sh 'aws cloudformation create-stack --stack-name ronynodegroup --template-body file://nodegroup.yml --region "us-east-1"' 
            }
        }
    }
}
