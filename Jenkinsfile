pipeline {
    agent any

    environment {
        MYSQL_USER = credentials('MYSQL_USER')
        MYSQL_PASSWORD = credentials('MYSQL_PASSWORD')
        MYSQL_DATABASE = credentials('MYSQL_DATABASE')
        MYSQL_ROOT_PASSWORD = credentials('MYSQL_ROOT_PASSWORD')
    }

    stages {
        stage('Clone repo') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Ayushi024/DevOps-Project-Two-Tier-Flask-App.git'
            }
        }

        stage('Build image') {
            steps {
                sh 'docker build -t flask-app .'
            }
        }

        stage('Deploy with docker compose') {
            steps {
                // stop existing containers if running
                sh 'docker compose down || true'

                // start app with Jenkins-injected env vars
                sh 'docker compose up -d --build'
            }
        }
    }
}
