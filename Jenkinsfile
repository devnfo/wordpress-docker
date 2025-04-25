pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = "wordpress_project"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/devnfo/wordpress-docker.git'
            }
        }

        stage('Stop Existing Containers') {
            steps {
                echo "Stopping existing containers if any..."
                bat "docker-compose down || exit 0"
            }
        }

        stage('Start Services with Docker Compose') {
            steps {
                echo "Starting services with docker-compose..."
                bat "docker-compose up -d"
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful!"
        }
        failure {
            echo "❌ Deployment failed!"
        }
    }
}
