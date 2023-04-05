pipeline {
    agent any
    stages {
        stage('Verify CloudFormation Template') {
            steps {
                sh 'aws cloudformation validate-template --template-body file://eks.yaml --region "us-east-1"' 
            }
        }
        stage('Create EKS Cluster') {
            steps {
                sh 'aws cloudformation create-stack --stack-name ronyEKS --template-body file://eks.yaml --region "us-east-1"' 
            }
        }
    }
}
