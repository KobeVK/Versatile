#!groovy


pipeline {
	agent any

	environment {
      branch = "${env.GIT_BRANCH}"
      evni = "${env.ENVIRONMENT}"
	}

	options {
		timestamps()
		// lock(evni)
	}

	stages {
		stage('prepare') {
			steps {
                withAWS(credentials: 'aws-access-key') {
					script {
						// if (branch == 'main') {
						// 	env.ENVIRONMENT = 'production'
						// } else {
						// 	env.ENVIRONMENT = 'staging'	
						// }
						sh """
							echo "Starting Terraform init"
							terraform init
							terraform plan -out myplan
							terraform apply
						"""
					}
				}
			}
		}

		stage('Test') {	
			steps {
				sh """
					echo "Hello, World!"
				"""
			}
		}

		stage('Deploy') {
			steps {
				sh """
					echo "kk"
				"""
				// sh "terraform apply -var 'environment=${evni}' -var 'tag_name=${env.GIT_BRANCH}'"
			}
		}

	}
}
