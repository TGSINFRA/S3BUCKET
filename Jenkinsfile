pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
    }
    
    stages {
        stage('CleanWorkspacefirst') {
            steps {
                cleanWs()
            }
        }
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/TGSINFRA/S3BUCKET.git'
            }
        }
        
        stage('Terraform command execution') {
            steps {
                script {
                    sh '''
                        #!/bin/bash
                        terraform init -backend-config region="us-east-1" -backend-config bucket="tgs-infra" -backend-config key="S3/mys3/terraform.tfstate"
                        terraform validate
                        terraform plan -var-file="configs/mys3/terraforms.tfvars"
                        terraform apply --auto-approve -var-file="configs/mys3/terraforms.tfvars"
                    '''
    }
            }
        }        
    stage('CleanWorkspace') {
            steps {
                cleanWs()
            }
        }   
    }
}
