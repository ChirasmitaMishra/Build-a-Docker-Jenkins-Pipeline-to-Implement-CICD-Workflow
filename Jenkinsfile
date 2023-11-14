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
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp chirasmita123/samplewebapp:latest'
                //sh 'docker tag samplewebapp chirasmita123/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "chirasmita123", url: "" ]) {
          sh  'docker push chirasmita123/samplewebapp:latest'
        //  sh  'docker push chirasmita123/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 chirasmita123/samplewebapp:latest"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://ubuntu@18.234.195.234 run -d -p 8003:8080 chirasmita123/samplewebapp:latest"
 
            }
        }
    }
	}
    
