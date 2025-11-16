pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Acedwdev/fullstack-docker-jenkins.git'
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                sh 'docker build -t backend-image ./backend'
            }
        }

        stage('Build Frontend Docker Image') {
            steps {
                sh 'docker build -t frontend-image ./frontend'
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                sh 'docker compose down'
                sh 'docker compose up -d'
            }
        }
    }
}
