pipeline {
    agent any

    environment {
        IMAGE_NAME = "php-website"
        CONTAINER_NAME = "php-container"
        REPO_URL = "https://github.com/kapil12333/Docker-PHP.git"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: "${REPO_URL}"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Stop Existing Container') {
            steps {
                script {
                    sh """
                    docker stop ${CONTAINER_NAME} || true
                    docker rm ${CONTAINER_NAME} || true
                    """
                }
            }
        }

        stage('Run New Container') {
            steps {
                script {
                    sh "docker run -d -p 8080:80 --name ${CONTAINER_NAME} ${IMAGE_NAME}"
                }
            }
        }

        stage('Cleanup Unused Docker Resources') {
            steps {
                script {
                    sh "docker system prune -f"
                }
            }
        }
    }

    post {
        success {
            echo "Deployment Successful! Your PHP site is running at http://your-server-ip:8080"
        }
        failure {
            echo "Build or Deployment Failed!"
        }
    }
}
