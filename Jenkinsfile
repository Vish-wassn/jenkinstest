pipeline {
    agent any
    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub-cred') 
    }
    
    stages {
        stage('checkoutcode') {
            steps {
                echo 'clone code'
                git 'https://github.com/Vish-wassn/node-demo.git' 
            }
        }
        
        stage('build image'){
            steps{
                echo 'creating the docker image'
                sh 'docker build -t vishudocker555/nodeapp1:$BUILD_NUMBER .' 
            }
        }
        stage('login to dockerhub'){
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR  --password-stdin'
            }
        }
        stage('push image and run th container'){
            steps{
                sh 'docker push vishudocker555/nodeapp1:$BUILD_NUMBER'
		sh 'docker run -d vishudocker555/nodeapp1:$BUILD_NUMBER'
            }
        }
    }
}
