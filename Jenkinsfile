pipeline {  
    agent any  
        stages { 
             stage("checkout") {  
           	    steps {  
                     git 'https://github.com/saikrishna308/onlinebookstore-master.git'
              	    }  
         	    } 
       	    stage("build") {  
           	    steps {  
                      echo " build successfully"  
                      sh "mvn clean package"
              	    }  
         	    } 
            stage("build docker Image") {  
           	    steps {  
                      sh "docker build -t onlinebook:1  ."
                      sh "docker tag onlinebook:1 saikrishna7842/onlinebook:3"
                      echo " build successfully"  
              	    }  
         	    } 
            stage("publish to registry") {
                steps {
                    withDockerRegistry(credentialsId: 'docker', url: 'https://hub.docker.com/') {
                           sh "docker push saikrishna7842/onlinebook:3"
                    }
                }

            }
        }
}
