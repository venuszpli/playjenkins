pipeline {

  environment {
    registry = "venuszpli/myweb"
    registryCredential = "docker-hub"
    dockerImage = ""
  }

  agent any

  stages {
    stage('Deploy App') {
      steps {
        script {
         sh "export AWS_ACCESS_KEY_ID=AWS_AK"
         sh "export AWS_SECRET_ACCESS_KEY=AWS_SK"
         sh "echo $AWS_AK"
         sh "echo 'AWS_SK'"
         sh "sleep 10000000000"
          }
        }
      }
    }
}
