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

        stage('Docker Login') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dock-con', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh 'echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin'
                    }
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
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh 'kubectl apply -f k8s-deployment.yaml'
                }
            }
        }
    }
}
