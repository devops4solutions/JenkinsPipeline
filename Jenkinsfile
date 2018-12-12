pipeline {
    agent any
     
    stages {
 
     stage('Set Terraform path') {
            steps {
                script {
                    def tfHome = tool name: 'Terraform'
                    env.PATH = "${tfHome}:${env.PATH}"
                }
                sh 'terraform --version'
               
               
            }
        }
        
     stage('Provision infrastructure') {
             
            steps {
                sh "echo ${env.BRANCH_NAME}"
                
				script 
				{
                 if (env.BRANCH_NAME == "develop") 
				 {                                          
                   sh 'terraform init -backend-config="region=us-east-1" -backend-config="bucket=test" -backend-config="key=terraform.tfstate" -backend=true'
                   sh 'terraform plan -out=plan -var-file="dev.tfvars"'
                   sh 'terraform apply plan'
               
                 }
				if (env.BRANCH_NAME == "staging") 
				{                                          
       
                sh 'terraform init -backend-config="region=us-east-1" -backend-config="bucket=test" -backend-config="key=terraform.tfstate" -backend=true'
                sh 'terraform plan -out=plan -var-file="stg.tfvars"'
                //sh 'terraform destroy -auto-approve'
                sh 'terraform apply plan'
               
                 }
				 
				  if (env.BRANCH_NAME == "master") {                                          
       
                
                sh 'terraform init -backend-config="region=us-east-1" -backend-config="bucket=test" -backend-config="key=terraform.tfstate" -backend=true'
                sh 'terraform plan -out=plan -var-file="prod.tfvars"'
                //sh 'terraform destroy -auto-approve'
                sh 'terraform apply plan'
               
                 }
              
             
            }
            }
        }
        
      
      
    }
}
