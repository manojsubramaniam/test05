pipeline{
	agent any 
        parameters {
           	 choice(name: 'BranchName', choices:['main','branch01'], description: 'to refresh the list, go to configure, disable "this build has parameters", launch build (without parameters)to reload the list and stop it, then launch it again (with parameters)')
	}
	
	stages{
		
	        stage("Run Tests") {
			steps {
			    sh "echo SUCCESS on ${BranchName}"
			}
		}
	
		stage('Checkout') {
			steps{
				checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '3cd686ab-1f5c-4dd9-9662-6ed1f11f2ef2', url: 'https://github.com/manojsubramaniam/test05.git']])
   		
			}
		}
		
	/*	
	         stage("Removing the Existing Container"){
		     	steps {
				
				sh '''
					docker stop $(docker ps -a -q --filter="name=nginx1234")
					docker rm $(docker ps -a -q --filter="name=nginx1234")
				'''
			}
		} */

		stage("build docker image"){
		     	steps {
				
				sh '''
					docker build -t nginx/nodeapp_test:latest .
					docker run -d --name nginx1234 -p 8000:80 nginx/nodeapp_test:latest
				'''
			}
		}
		

		stage("docker container"){
			steps {
				echo'running docker image into container..'
			}
		}
	
	}
}
