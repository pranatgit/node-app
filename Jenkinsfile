pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
    }
    stages{
        stage('Build Docker Image'){
            steps{
                sh "docker build . -t pranatdocker/nodeapp:${DOCKER_TAG} "
            }
        }
        stage('DockerHub Push'){
            steps{
                withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerHubPwd')]) {
                    sh "docker login -u pranatdocker -p ${dockerHubPwd}"
                    sh "docker push pranatdocker/nodeapp:${DOCKER_TAG}"
                }
            }
        }
        stage('Deploy to DevServer'){
            steps{
               echo "Deploying to DevServer"
            }
        }
    }
}

def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}
