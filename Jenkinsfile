pipeline {
    agent any
    stages {
        stage('Create EKS Cluster and Nodegroup') {
            steps {
                sh 'aws cloudformation create-stack --stack-name ronyEKS --template-body file://eks.yaml --region "us-east-1"' 
            }
        }
        
        stage('Deploy Application') {
            environment {
                KUBECONFIG = "kubeconfig.yaml"
            }
            steps {
                sh 'kubectl apply -f deploy.yml -f service.yml'
            }
        }
    }
}
