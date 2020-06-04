pipeline {

  environment {
    registry = "venuszpli/myweb"
    registryCredential = "docker-hub"
    dockerImage = ""
    AWS_ACCESS_KEY_ID = "AKIA2YDUCZG64ZT4CDAQ"
    AWS_SECRET_ACCESS_KEY = "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"
    AWS_DEFAULT_REGION = "ap-northeast-1"
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
          withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'AWS_AK_SK', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
              kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "mykubeconfig")
          }
        }
      }
    }

  }

}
