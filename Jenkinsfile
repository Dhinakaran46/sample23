pipeline{
    agent any

      environment {
        DOCKER_IMAGE = 'dhinakarandk/sample23'
    }
    stages{
        stage('pull code'){
            steps {
                echo 'pulling code from git hub'
                checkout scm
            }
        }
        stage('Check Docker') {
           steps {
             bat 'docker context ls'
              bat 'docker info'
            }
        }
        stage('Build Docker image'){
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}")
                }
                echo 'image created'
            }
        }
       stage('Push to Docker Hub') {
        steps {
            withCredentials([usernamePassword(
              credentialsId: 'dockerhub-credentials',
               usernameVariable: 'DOCKER_USER',
              passwordVariable: 'DOCKER_PASS'
        )]) {
            bat '''
                @echo off
                echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin
                docker push %DOCKER_IMAGE%
            '''
            }
       }
    }
    
}
}
