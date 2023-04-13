pipeline {
    agent any
	
	  tools
    {
       maven "maven-3.6.3"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/devops4solutions/CI-CD-using-Docker.git'
             
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
                sh 'docker tag samplewebapp janajohny/samplewebapp:latest'
                //sh 'docker tag samplewebapp nikhilnidhi/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "docker", url: "" ]) {
          sh  'docker push janajohny/samplewebapp:latest'
          //sh  'docker push janajohny/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 janajohny/samplewebapp"
 
            }
        }
 //stage('Run Docker container on remote hosts') {
             
          //  steps {
                //sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 8003:8080 janajohny/samplewebapp"
 
           // }
        //}
    }
	}
    
