pipeline {
    agent {
        label 'docker-cd-agent'
    }
    environment {
        IMAGE = "gurkiran24/flask-app"
        TAG   = "latest"
    }
    stages {
        stage('Check Docker') {
            steps {
                sh '''
                    docker --version
                    docker ps
                '''
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKER_USERNAME',
                        passwordVariable: 'DOCKER_PASSWORD'
                    )
                ]) {
                    sh '''
                        echo "$DOCKER_PASSWORD" | docker login \
                        -u "$DOCKER_USERNAME" \
                        --password-stdin
                    '''
                }
            }
        }
        stage('Pull Latest Image') {
            steps {
                sh '''
                    docker pull ${IMAGE}:${TAG}
                '''
            }
        }
        stage('Stop Old Container') {
            steps {
                sh '''
                    docker rm -f flaskapp || true
                '''
            }
        }
        stage('Deploy New Container') {
            steps {
                sh '''
                    docker run -d \
                    --name flaskapp \
                    -p 5000:5000 \
                    ${IMAGE}:${TAG}
                '''
            }
        }
        stage('Verify Deployment') {
            steps {
                sh '''
                    docker ps
                '''
            }
        }
    }

    post {
        success {
            echo "Flask app deployed successfully!"
        }
        failure {
            echo "Deployment failed!"
        }
        always {
            sh 'docker logout || true'
        }
    }
}
