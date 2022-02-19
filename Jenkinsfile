pipeline {
    agent {
        label 'slave1'
    }
    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/farooq-cloud/sample-nodejs.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'sudo docker build -t farooq786/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'sudo docker push farooq786/nodeapp:$BUILD_NUMBER '
            }
        }
        stage('docker run') {
            steps{
                sh 'sudo docker rm -f con1'
                sh 'sudo docker run -itd --name con1 -p 3000:3000 farooq786/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

