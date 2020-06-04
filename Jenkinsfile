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
          withCredentials([string(credentialsId: 'AWS_AK', variable: 'aws_ak'), string(credentialsId: 'AWS_SK', variable: 'aws_sk')]) {
             kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "mykubeconfig")
          }
          }
        }
      }
    }

  }

}
