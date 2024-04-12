pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerHub')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git url: 'https://github.com/shruti-102/.net-app.git', branch: 'master'
            }
        }
 
        stage('Build docker image') {
            steps {  
                sh 'docker build -t shrutishukla102/devops:$BUILD_NUMBER .' 
            }
        }
        stage('login to dockerHub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push shrutishukla102/devops:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}