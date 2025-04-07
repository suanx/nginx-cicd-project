pipeline {
    agent any

    environment {
        dckrimg = 'nginx/webapp:latest'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git url: 'https://github.com/suanx/nginx-cicd-project.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${dckrimg} ."
                }
            }
        }
    }

    post {
        success {
            echo '✅ Docker image built successfully!'
        }
        failure {
            echo '❌ Build failed. Check logs for errors.'
        }
    }
}
