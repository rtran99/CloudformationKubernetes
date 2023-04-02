pipeline {
    agent any
    stages {
        stage('Verify CloudFormation Template') {
            steps {
                sh 'aws cloudformation validate-template --template-body file://cloudformation/eks-cluster.yaml'
            }
        }
        stage('Create EKS Cluster') {
            steps {
                sh 'aws cloudformation create-stack --stack-name my-eks-cluster --template-body file://cloudformation/eks.yaml'
                sh 'aws cloudformation wait stack-create-complete --stack-name my-eks-cluster'
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
