pipeline {
    agent any

    environment {
        FLASK_APP = 'AiService.py'
        PYTHON_VERSION = '3.6'
    }

    stages {
        stage('Build') {
            steps {
                script {
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