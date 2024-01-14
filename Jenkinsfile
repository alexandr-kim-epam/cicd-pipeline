pipeline {
  agent any
  environment {
    DOCKERHUB_CREDENTIALS = 'dhtraining'
  }  
  stages {
    stage('Git Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/alexandr-kim-epam/cicd-pipeline.git'
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
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin docker.io'
                sh 'docker push kim26557/training_cicd:$BUILD_NUMBER'
                sh 'docker logout'
                //sh 'docker run -d -p 3000:3000 --name training_cicd-container kim26557/training_cicd:${BUILD_NUMBER}'
            }
        }
    }    
    
  }
}
