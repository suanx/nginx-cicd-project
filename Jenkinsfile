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

        stage('Run Docker Container') {
            steps {
                script {
                    sh "docker run -d -p 9001:80 --name webapp ${dckrimg}"
                }
            }
        }
    }
}
