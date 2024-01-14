pipeline {
  agent any
  stages {
    stage('Git Checkout') {
      steps {
        git(branch: 'main', url: 'https://github.com/alexandr-kim-epam/cicd-pipeline', credentialsId: 'dhtraining')
      }
    }

  }
  environment {
    DOCKERHUB_CREDENTIALS = 'dhtraining'
  }
}