pipeline{
	agent{ label 'JDK17' }
	options { 
		timeout(time: 1, unit: 'HOURS') 
		retry(2)
	}
	triggers { 
		cron('0 * * * *') 
	}
	parameters{
		choice(name: 'GOAL',choices: ['compile','package','clean package'])
	}
	stages{
		stage('Source Code'){
			steps{
				git url: 'https://github.com/sanjushyam001/spring-petclinic.git' ,branch: 'main'	
			}
		}
		stage('Build the code'){
			steps{
				
				sh script: "/opt/apache-maven-3.9.1/bin/mvn ${params.GOAL}"
			}
		}
		stage('Reporting and Archiving'){
			steps{
				junit testResults: 'target/surefire-reports/*.xml'
			}
		}
	}
	post{
		success {
			//send the success email
			echo "Success"
		}
		unsuccessful{
			//send the unseccess email
			echo "Failure"
		}
	}
}
