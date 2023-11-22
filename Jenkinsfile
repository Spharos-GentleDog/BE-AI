pipeline {
    agent any

    environment {
        FLASK_APP = 'AiService.py'
        PYTHON_VERSION = '3'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    sh "apt-get update && apt-get install -y python${PYTHON_VERSION} python${PYTHON_VERSION}-dev"
                    sh 'pip install -r requirements.txt'
                }
            }
        }
        stage('DockerSize') {
            steps {
                sh '''
                    docker stop flask || true
                    docker rm flask || true
                    docker rmi flask || true
                    docker build -t flask .
                    echo "flask: build success"
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                docker run -d --name flask --network gentledog flask
                echo "flask: run success"
                '''
                }
        }
    }
}