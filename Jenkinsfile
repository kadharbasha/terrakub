pipeline {
 	agent any
 	stages {
 		stage('checkout') {
 			steps {
 				git(
           url: 'https://github.com/kadharbasha/monorep.git',
           credentialsId: '01',
           branch: 'master'
        )
 			}
 		}
 		stage('Set Terraform path') {
	 		steps {
	 			script {
	 				def tfHome = tool name: 'Terraform'
	 				env.PATH = "${tfHome}:${env.PATH}"
 				}
	 			sh 'terraform — version'
	 		}
	 	}
 		stage('Provision infrastructure') {
 			steps {
 				dir('services/dir1') {
 					sh 'terraform init'
 					sh 'terraform plan -out=plan'
 					// sh 'terraform destroy -auto-approve'
					sh 'terraform apply plan'
 				}	
 			}
 		}
	}
}
