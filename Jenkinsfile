pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('kaushi-dockerhub')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/Kaushi22k/connect.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t kaushi22k/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push kaushi22k/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
