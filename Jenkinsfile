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
                sh 'aws cloudformation create-stack --stack-name ronyEKS --template-body file://eks.yaml'
                sh 'aws cloudformation wait stack-create-complete --stack-name ronyEKS'
            }
        }
        stage('Configure kubectl') {
            steps {
                sh 'aws eks update-kubeconfig --name my-eks-cluster'
            }
        }
        stage('Deploy Kubernetes Manifests') {
            steps {
                sh 'kubectl apply -f kubernetes-manifests'
            }
        }
    }
}
