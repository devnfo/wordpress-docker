pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/devnfo/wordpress-docker.git'
            }
        }
        stage('Build & Run Docker') {
            steps {
                script {
                    sh 'docker-compose down || true'
                    sh 'docker-compose up -d --build'
                }
            }
        }
    }
}
