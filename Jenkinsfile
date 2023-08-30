pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-ashok513068')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git ''
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t udaychinnala/nodeapp1:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push udaychinnala/nodeapp1:$BUILD_NUMBER'
            }
        }
        stage('pull image') {
            steps{
                sh 'docker pull udaychinnala/nodeapp1:$BUILD_NUMBER'
            }
        }
      stage('run image') {
            steps{
                sh 'docker run -d -p 443:80 udaychinnala/nodeapp1:$BUILD_NUMBER'
            }
        }   
}
post {
        always {
            sh 'docker logout'
        }
    }
}

