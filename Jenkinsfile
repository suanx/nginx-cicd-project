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

        stage('docker push-dckrimg -to hub') {
            steps {
                script {
                    sh "docker push $(dckrimg)"
            }
        }
    }
}
