pipeline {
  agent any
  stages {
    stage('Git Checkout') {
      steps {
        git(branch: 'main', url: 'https://github.com/alexandr-kim-epam/cicd-pipeline', credentialsId: 'dhtraining')
      }
    }

    stage('App Build') {
      steps {
        sh 'script scripts/build.sh'
      }
    }

    stage('Tests') {
      steps {
        sh 'script scripts/test.sh'
      }
    }

  }
  environment {
    DOCKERHUB_CREDENTIALS = 'dhtraining'
  }
}