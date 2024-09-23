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
                      sh "mvn clean install"
                      echo " build successfully"    
              	    }  
         	    } 
            stage("build docker Image") {  
           	    steps {  
                      sh "docker build -t onlinebooks ."
                      sh "docker tag onlinebooks:3 saikrishna7842/onlinebooks:3"
                      echo " build successfully"  
              	    }  
         	    }
             stage("publish to registry") {
                steps {
                    withDockerRegistry(credentialsId: 'docker', url: 'https://hub.docker.com/repositories/saikrishna7842') {
                           sh "docker push saikrishna7842/onlinebooks:3"
                    }
                }
             }
        }
}
