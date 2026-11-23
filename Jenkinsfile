pipeline{
    agent:any

      environment {
        DOCKER_IMAGE = 'dhinakarandk/sample23'
    }
    stages{
        stage('pull code'){
            steps{
                echo 'pulling code from git hub'
                checkout scm
            }
        }
        stage('Build Docker image'){
            step{
                script{
                    docker.build("${DOCKER_IMAGE}")
                }
                echo 'image created'
            }
        }
        stage('push to docker hub'){
            step{
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        docker.image("${DOCKER_IMAGE}").push()
                    }
                
            }
        }

    }
    
    }
}
