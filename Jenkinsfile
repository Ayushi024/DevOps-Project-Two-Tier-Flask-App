pipeline {
    agent any

    environment {
        MYSQL_USER = credentials('MYSQL_USER')
        MYSQL_PASSWORD = credentials('MYSQL_PASSWORD')
        MYSQL_DATABASE = credentials('MYSQL_DATABASE')
        MYSQL_ROOT_PASSWORD = credentials('MYSQL_ROOT_PASSWORD')
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh '''
                  echo "Workspace content:"
                  ls -la
                  docker build -t flask-app .
                '''
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                sh '''
                  docker-compose down || true
                  docker-compose up -d --build
                '''
            }
        }
    }
}
