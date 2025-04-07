pipeline {
    agent any

    environment {
        dckrimg = 'suanx/webapp:latest'
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

        stage('Push Docker Image to Hub') {
            steps {
                script {
                    sh "docker push ${dckrimg}"
                }
            }
        }
    }

    post {
        success {
            echo '✅ Docker image built and pushed to Docker Hub!'
        }
        failure {
            echo '❌ Something went wrong. Check the logs.'
        }
    }
}
