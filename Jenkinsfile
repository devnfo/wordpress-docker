pipeline {
    agent any

    environment {
        IMAGE_NAME = 'wordpress'
        CONTAINER_NAME = 'wordpress-container'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/devnfo/wordpress-docker.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Stop Existing Container') {
            steps {
                script {
                    def result = bat(script: "docker ps -q -f name=%CONTAINER_NAME%", returnStdout: true).trim()
                    if (result) {
                        bat "docker stop %CONTAINER_NAME%"
                        bat "docker rm %CONTAINER_NAME%"
                    } else {
                        echo "No running container named %CONTAINER_NAME% found."
                    }
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                bat 'docker run -d -p 8080:80 --name %CONTAINER_NAME% %IMAGE_NAME%'
            }
        }
    }

    post {
        always {
            echo "Pipeline execution complete."
        }
        success {
            echo "Deployment successful."
        }
        failure {
            echo "Deployment failed."
        }
    }
}
