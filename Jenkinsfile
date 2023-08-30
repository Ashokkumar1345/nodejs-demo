pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-ashok513068')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/Ashokkumar1345/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t ashok513068/nodeapp1:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push ashok513068/nodeapp1:$BUILD_NUMBER'
            }
        }
        stage('pull image') {
            steps{
                sh 'docker pull ashok513068/nodeapp1:$BUILD_NUMBER'
            }
        }
      stage('run image') {
            steps{
                sh 'docker run -d -p 443:80 ashok513068/nodeapp1:$BUILD_NUMBER'
            }
        }   
}
post {
        always {
            sh 'docker logout'
        }
    }
}

