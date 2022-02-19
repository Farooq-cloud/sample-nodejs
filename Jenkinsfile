pipeline {
    agent {
        label 'slave1'
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/Farooq-cloud/sample-nodejs.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t Farooq/nodeapp:1 .'
            }
        }
        
        
}

}

