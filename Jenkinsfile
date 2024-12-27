pipeline {
    agent any
    tools {
        terraform 'Terraform-Jenkins'
    }

    stages {
        stage('Check for Azure CLI') {
            steps{
                script {
                    sh 'command -v az > /dev/null 2>&1 && az --version || curl -sL https://aka.ms/InstallAzureCLIDeb | bash'
                }
            }
        }
        stage('terraform init') {
            steps {
                script {
                    echo 'Init Stage'
                    sh 'terraform init'
                }
            }
        }
        stage('terraform plan') {
            steps {
                script {
                    echo 'Plan Stage'
                    withCredentials([azureServicePrincipal('AZURE_CRED')]) {
//                    sh 'terraform plan -var "subs_id=$AZURE_SUBSCRIPTION_ID" -var "tenant_id=$AZURE_TENANT_ID" -var "client_id=$AZURE_CLIENT_ID" -var "client_secret=$AZURE_CLIENT_SECRET"'
                     sh 'terraform plan'
                    }
                }
            }
        }
        stage('terraform apply') {
            steps {
                script {
                    echo 'Apply Stage'
                }
            }
        }
        stage('function deploy') {
            steps {
                script {
                    echo 'Function Deploy Stage'
                }
            }
        }
        stage('cleanup') {
            steps {
                script {
                    echo 'Cleanup Stage'
                }
            }
        }
    }
}
