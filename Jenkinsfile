pipeline {
  environment {
    registry = "docker_hub_account/repository_name"
    registryCredential = 'dockerhub'
  }
  agent any
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry("https://176065828214.dkr.ecr.us-east-1.amazonaws.com/my_application") {
            dockerImage.push()
          }
        }
      }
    }
}
