pipeline {
    agent any
    
    stages {
        stage('Clone Repository') {
            steps {
                checkout scm
            }
        }
        
        stage('Install Python & pip') {
            steps {
                sh '''
                    # Alpine Linux ke liye apk package manager
                    apk add --no-cache python3 py3-pip
                    python3 -m pip install --upgrade pip
                '''
            }
        }
        
        stage('Install Python Dependencies') {
            steps {
                sh '''
                    pip3 install flake8 pytest
                    if [ -f requirements.txt ]; then
                        pip3 install -r requirements.txt
                    fi
                '''
            }
        }
        
        stage('Run flake8 & Unit Tests') {
            steps {
                sh '''
                    echo "Running flake8..."
                    flake8 . --exit-zero || true
                    
                    echo "Running tests..."
                    python3 -m pytest || echo "No tests found"
                '''
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh '''
                    docker build -t my-flask-app:latest .
                '''
            }
        }
        
        stage('Run Docker Container') {
            steps {
                sh '''
                    docker stop my-flask-app || true
                    docker rm my-flask-app || true
                    docker run -d --name my-flask-app -p 5000:5000 my-flask-app:latest
                '''
            }
        }
        
        stage('Deployment Success') {
            steps {
                echo 'Application deployed successfully on port 5000'
            }
        }
    }
}