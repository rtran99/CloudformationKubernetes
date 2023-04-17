pipeline {
    agent any
    stages {
        stage('Create EKS Cluster and Nodegroup') {
            steps {
                script {
                    def stackExists = sh(script: "aws cloudformation describe-stacks --stack-name ronyEKS --region \"us-east-1\" --query \"Stacks[].StackName\" --output text || true", returnStdout: true).trim()
                    if (stackExists) {
                        echo "EKS stack already exists. Skipping creation."
                    } else {
                        sh 'aws cloudformation create-stack --stack-name ronyEKS --template-body file://eks.yaml --region "us-east-1"' 
                        sh 'aws cloudformation wait stack-create-complete --stack-name ronyEKS --region "us-east-1"'
                    }
                }
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
