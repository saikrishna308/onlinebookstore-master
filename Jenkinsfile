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
                      bat 'mvn clean install'
                      echo " build successfully"    
              	    }  
         	    } 
            stage("build docker Image") {  
           	    steps {  
                      bat 'docker build -t onlinebooks .'
                      bat "docker tag onlinebooks:latest saikrishna7842/onlinebooks:3"
                      echo " build image successfully"  
              	    }  
         	    }
             stage("publish to registry") {
                steps {
                      withDockerRegistry(credentialsId: 'docker', url:'https://index.docker.io/v1/'){
                           bat "docker push saikrishna7842/onlinebooks:3"
                    }
                }
             }
            stage("deployment") {
                steps {
                    bat 'kubectl apply -f .\deployment.yaml'
                    echo "deployment successfully"
                }
        }
        }
}
