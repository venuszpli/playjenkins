pipeline {

  environment {
    registry = "venuszpli/myweb"
    registryCredential = "docker-hub"
    dockerImage = ""
    AWS_ACCESS_KEY_ID = credentials('AWS_AK')
    AWS_SECRET_ACCESS_KEY = credentials('AWS_SK')
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
        sh "aws s3 ls"
        sh "whoami"
        sh "pwd"
        sh "ls -lah "
        sh "sleep 1000000000"        
        script {
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "mykubeconfig")
                }
            }
        }
    }
}
