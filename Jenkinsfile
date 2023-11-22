pipeline {
    agent any

    environment {
        FLASK_APP = 'AiService.py'
        FLASK_ENV = 'production'
        PYTHON_VERSION = '3.6'
    }

    stages {
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
                docker run -e FLASK_APP="${FLASK_APP}" -e FLASK_ENV="${FLASK_ENV}" -d --name flask --network gentledog flask
                echo "flask: run success"
                '''
                }
        }
    }
}