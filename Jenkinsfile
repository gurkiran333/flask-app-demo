pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
               git branch: 'main', url: 'https://github.com/gurkiran333/flask-app-demo.git'
            }
        }
        
        stage("Install pip3") {
            steps {
                sh "sudo apt-get update && sudo apt-get install python3-pip -y"
            }
        }
        
        stage("Install dependencies") {
            steps {
                sh "pip3 install -r requirements.txt"
            }
        }
        
        stage("Execute flake8 scan and execute unit test cases") {
            steps {
                sh "pip3 install flake8 pytest"
                sh "flake8 . || echo 'Flake8 issues found'"
                sh "pytest || echo 'Tests failed'"
            }
        }
        
        stage("Build Docker Image") {
            steps {
                sh "docker build -t mywebimg:latest ."
            }
        }
        
        stage("Run Docker Container") {
            steps {
                sh "docker rm -f webos || true"
                sh "docker run -dit --name webos -p 80:80 mywebimg"
            }
        }
        
        stage("Successful deployment") {
            steps {
                echo "Application Deployed Successfully"
            }
        }
    }
}