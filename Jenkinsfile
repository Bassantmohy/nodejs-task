pipeline {
    agent any

    environment {
        IMAGE_NAME = "nodejs-task:${env.BUILD_NUMBER}"
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out source code..."
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                script {
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Run Container') {
            steps {
                echo "Running container..."
                script {
                    sh '''
                        if docker ps -a --format '{{.Names}}' | grep -Eq "^${IMAGE_NAME}\$"; then
                            docker rm -f ${IMAGE_NAME} || true
                        fi
                        docker run -d --name ${IMAGE_NAME} -p 3000:3000 ${IMAGE_NAME}
                    '''
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline finished ✅"
        }
    }
}
