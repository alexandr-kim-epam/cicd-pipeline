pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS=credentials('dhtraining')
    }
    stages{
        stage("Git Checkout"){
            steps{
                git branch: 'main', url: 'https://github.com/alexandr-kim-epam/cicd-pipeline.git'
            }
        }

        stage('App Build') {
            steps {
                sh 'script scripts/build.sh'
            }
        }

        stage('Test') {
            steps {
                sh 'script scripts/test.sh'
            }
        }

        stage('Node.js App Build') {
            steps {
                scripts {
                    def nodeAppDockerfilePath = 'Dockerfile'
                    sh "docker build -t alexandr-kim-epam/nodeapp:$BUILD_NUMBER -f ${nodeAppDockerfilePath} ."
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin docker.io'
                    sh 'docker push alexandr-kim-epam/nodeapp:$BUILD_NUMBER'
                    sh 'docker logout'
                    sh "docker run -d -p 3000:3000 --name nodeapp-container alexandr-kim-epam/nodeapp:$BUILD_NUMBER"
                }
            }
        }
    }
}