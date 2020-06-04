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
        sh "export AWS_ACCESS_KEY_ID=AKIA2YDUCZG64ZT4CDAQ"
        sh "export AWS_SECRET_ACCESS_KEY=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"
        sh "export AWS_DEFAULT_REGION=ap-northeast-1"
        script {
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}
