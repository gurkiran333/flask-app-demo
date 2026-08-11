pipeline {
    agent any

    stages {
        stage('Setup Environment') {
            steps {
                sh '''
                    apt-get update
                    apt-get install -y python3 python3-pip docker.io
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    pip3 install -r requirements.txt
                    pip3 install flake8 pytest
                '''
            }
        }

        stage('Code Quality and Unit Tests') {
            steps {
                sh '''
                    python3 -m flake8 .
                    python3 -m pytest
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    docker build -t flask-app:latest .
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                    docker rm -f flask-app || true
                    docker run -d --name flask-app -p 5000:5000 flask-app:latest
                '''
            }
        }

        stage('Successful Deployment') {
            steps {
                echo 'Flask application deployed successfully!'
            }
        }
    }
}