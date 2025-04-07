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
            stage('To test build locally')
            steps {
                sh "docker run -d -p 9001:80 --name webapp ${dckrimg}
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
