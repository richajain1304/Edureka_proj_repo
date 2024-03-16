
pipeline{
    tools{
       
        maven 'mymaven'
    }
    environment{
	    DOCKERHUB_CREDENTIALS=credentials('dockerhub_cred')
	    registry = "richajain473/edureka_proj"
	    registryCredential = 'dockerhub_cred'
            dockerImage = ''
    }
	agent any
      stages{
           stage('Checkout the code'){
	    
               steps{
		 echo 'cloning the repo'
                 git 'https://github.com/richajain1304/Edureka_proj_repo.git'
              }
          }
          stage('Compile'){
             
              steps{
                  echo 'complie the code again..'
                  sh 'mvn compile'
	      }
          }
          stage('CodeReview'){
		  
              steps{
		    
		  echo 'codeReview'
                  sh 'mvn pmd:pmd'
              }
          }
           stage('UnitTest'){
		  
              steps{
	         
                  sh 'mvn test'
              }
          
          }
        
          stage('Package'){
		  
              steps{
		  
                  sh 'mvn package'
              }
          }
	 stage('copy ar file to current dir'){
		 steps{
		   sh 'cp /var/lib/jenkins/workspace/Edureka_proj/target/addressbook.war .'
		 }
		 
	 }
        stage('Building our image') {
             steps{
                   script {
                         dockerImage = docker.build registry + ":$BUILD_NUMBER"
                   }
            }
        }  
      }
}
