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

        stage('Deploy with Docker Compose') {
            steps {
                sh """
                    echo '=== Deploying with Docker Compose ==='
                    
                    # Bajar el stack si existe, pero sin fallar si no está levantado
                    docker-compose down || true

                    # Levantar todo nuevamente
                    docker-compose up -d --build
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
