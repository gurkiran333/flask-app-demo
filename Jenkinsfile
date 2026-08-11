pipeline {
    agent any

    stages {
        stage('Setup Environment') {
            steps {
                sh '''
                    apt-get update
                    apt-get install -y python3 python3-pip python3-venv docker.io
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    # Virtual environment banayein
                    python3 -m venv venv
                    
                    # Activate aur packages install karein
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                    pip install flake8 pytest
                '''
            }
        }

        stage('Code Quality and Unit Tests') {
            steps {
                sh '''
                    . venv/bin/activate
                    flake8 .
                    pytest
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
                    docker run -d \
                        --name flask-app \
                        -p 5000:5000 \
                        --restart=always \
                        flask-app:latest
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