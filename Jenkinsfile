pipeline {
    agent any

    stages {
        stage('Download/clone the source repo from github') {
            steps {
               git branch: 'main', url: 'https://github.com/gurkiran333/flask-app-demo.git'
            }
        }
        
        stage("Install pip3") {
            steps{
                sh "apt-get update && apt-get install python3-pip -y"
            }
        }
        
        stage("Install dependencies") {
            steps{
                sh "pip3 install -r requirements.txt"
            }
        }
        
        stage("Execute flake8 scan and execute unit test cases") {
            steps{
                sh "pip3 install flake8 pytest"
                sh "flake8 . || true"  // || true means ignore errors
                sh "pytest || true"
            }
        }
        
        stage("Build Docker Image") {
            steps{
                sh "docker build -t mywebimg:latest ."
            }
        }
        
        stage("Run Docker Container") {
            steps{
                sh "docker rm -f webos || true"
                sh "docker run -dit --name webos -p 80:80 mywebimg"
            }
        }
        
        stage("Successful deployment") {
            steps{
                echo "Application Deployed Successfully"
            }
        }
    }
}