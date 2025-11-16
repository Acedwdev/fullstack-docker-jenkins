pipeline {
    agent any

    environment {
        BACKEND_IMAGE = "backend-image"
        FRONTEND_IMAGE = "frontend-image"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Acedwdev/fullstack-docker-jenkins.git'
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                sh """
                    echo '=== Building Backend Image ==='
                    docker build -t $BACKEND_IMAGE ./backend
                """
            }
        }

        stage('Build Frontend Docker Image') {
            steps {
                sh """
                    echo '=== Building Frontend Image ==='
                    docker build -t $FRONTEND_IMAGE ./frontend
                """
            }
        }

        stage('Deploy') {
            steps {
                sh """
                    echo '=== Rebuilding backend & frontend ==='

                    docker-compose build backend frontend
                    docker-compose up -d backend frontend
                """
            }
        }
    }

    post {
        failure {
            echo "El pipeline falló. Revisa los logs arriba."
        }
        success {
            echo "Pipeline ejecutado con éxito"
        }
    }
}
