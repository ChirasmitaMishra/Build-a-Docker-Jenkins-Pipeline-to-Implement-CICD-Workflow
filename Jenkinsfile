pipeline {
    agent any	
    environment {
    DOCKERHUB_CREDENTIALS = credentials('chirasmita123')
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'main', url: 'https://github.com/ChirasmitaMishra/Jenkins-Docker-Project.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

       stage('Build docker image') {
            agent { label 'docker-agent' }
            steps {  
                sh 'docker build -t chirasmita123/samplewebapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
	    agent { label 'docker-agent' }
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
	    agent { label 'docker-agent' }
            steps{
                sh 'docker push chirasmita123/samplewebapp:$BUILD_NUMBER'
            }
        }
             
      stage('Run Docker container on Jenkins Agent') {
            agent { label 'docker-agent' }
            steps {
                sh "docker run -d -p 8003:8080 chirasmita123/samplewebapp:$BUILD_NUMBER"
             }
        }
     }
}
    
