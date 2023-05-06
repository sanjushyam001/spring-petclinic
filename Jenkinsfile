pipeline{
	agent{ label 'JDK17' }
	options { 
		timeout(time: 1, unit: 'HOURS') 
		retry(2)
	}
	triggers { 
		cron('0 * * * *') 
	}
	stages{
		stage('Source Code'){
			steps{
				git url: 'https://github.com/sanjushyam001/spring-petclinic.git',branch: 'main'	
			}
		}
		stage('Build the code'){
			steps{
				sh script: "mvn clean package"
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
