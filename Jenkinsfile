pipeline {

  environment {
    registry = "venuszpli/myweb"
    registryCredential = "docker-hub"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/venuszpli/playjenkins.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "", registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }

    stage('Deploy App') {
      steps {
        script {
         sh "export AWS_ACCESS_KEY_ID=AWS_AK"
         sh "export AWS_SECRET_ACCESS_KEY=AWS_SK"
         sh "echo $AWS_ACCESS_KEY_ID"
         sh "sleep 10000000000"
          }
        }
      }
    }
}
