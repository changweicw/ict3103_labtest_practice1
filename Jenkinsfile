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
        stage("build"){
            steps{
                sh 'docker build -t changweicw/labtest1:latest .'
            }
        }
        stage("deploy"){
            steps{
                sh 'docker ps -f name=savemepls | grep -o "savemepls" && docker kill $(docker ps -f name=savemepls | grep -o "savemepls")'
                sh "printf 'y' | docker container prune"
                sh 'docker run -d -p 127.0.0.1:3389:3389 --name savemepls changweicw/labtest1:latest'
            }
        }

       
    }
}
