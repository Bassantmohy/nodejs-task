pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t nodejs-task:4 .'
            }
        }

        stage('Run Container') {
            steps {
                echo 'Running container...'
                // احذفي أي container قديم بنفس الاسم قبل ما تشغلي الجديد
                sh 'docker rm -f nodejs-task-4 || true'
                sh 'docker run -d --name nodejs-task:4 -p 3001:3001 nodejs-task:4'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished ✅'
        }
    }
}
