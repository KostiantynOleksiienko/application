pipeline {
  environment {
    registry = "kote/my-application"
    dockerImage = ''
  }
  agent any
  stages {
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Build') {
      steps {
        sh '$(aws --region us-east-1 ecr get-login --no-include-email)'
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
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}
