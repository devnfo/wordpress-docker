pipeline {
    agent any

    environment {
        GIT_CREDENTIALS_ID = 'github-creds'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git credentialsId: "${GIT_CREDENTIALS_ID}", url: 'https://github.com/devnfo/wordpress-docker.git', branch: 'main'
            }
        }

        stage('Build & Run Docker') {
            steps {
                sh 'docker compose up -d --build'
            }
        }
    }
}
