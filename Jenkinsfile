pipeline {  
    agent any
    environment {
        DOCKER_USERNAME = credentials('docker-username') // Replace with your Jenkins credential ID
        DOCKER_PASSWORD = credentials('docker-password') // Replace with your Jenkins credential ID
    }
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
                      sh "docker tag onlinebooks:latest saikrishna7842/onlinebooks:3"
                      echo " build successfully"  
              	    }  
         	    }
             stage("publish to registry") {
                steps {
                     sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin'{
                           sh "docker push saikrishna7842/onlinebooks:3"
                    }
                }
             }
        }
}
