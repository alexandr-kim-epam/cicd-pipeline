pipeline {
  agent {
    node { label 'slavefordocker'}  
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('docker_hub_cred')
  }
  stages {
    stage('Git Checkout') {
      steps {
        git(branch: 'main', url: 'https://github.com/alexandr-kim-epam/cicd-pipeline.git', credentialsId: 'git_cred')
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

    stage('Node.js App Build') {
      steps {
        script {
          sh 'docker build -t kim26557/training_cicd:${BUILD_NUMBER} .'
          sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
          sh 'docker push kim26557/training_cicd:$BUILD_NUMBER'
          sh 'docker logout'
        }

      }
    }

  }
}
