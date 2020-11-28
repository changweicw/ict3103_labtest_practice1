pipeline {
    agent any 
    stages {
        stage('Static Analysis') {
            steps {
                echo 'Run the static analysis to the code' 
            }
        }
        stage('Compile') {
            agent {
                docker {
                    image 'python:3.8'
                }
            }
            steps {
                echo 'Compile the source code' 
                 sh 'pip install -r requirements.txt'
            }
        }
        stage('Checkout SCM') {
			steps {
				git '/home/JenkinsDependencyCheckTest'
			}
		}

		stage('OWASP DependencyCheck') {
			steps {
				dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'Default'
			}
		}
        stage("build"){
            steps{
                sh 'docker build -t changweicw/labtest1:latest .'
            }
        }
       
    }
    post {
		success {
			dependencyCheckPublisher pattern: 'dependency-check-report.xml'
		}
	}
}
