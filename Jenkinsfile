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
        stage('push to docker hub'){
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        docker.image("${DOCKER_IMAGE}").push()
                    }
                
            }
        }

    }
    
    }
}
