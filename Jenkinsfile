pipeline{
    agent any
    environment{
        dckrimg = 'nginx/webapp:latest'
    }
    stages{
        stage('git checkout ') {
            steps{
            git url: 'https://github.com/suanx/nginx-cicd-project.git',branch: 'main'
        }
    }
    stage('build docker image'){
        steps{
            sh 'docker build -t $dckrimg .'
        }
    }
}
}
