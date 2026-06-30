pipeline {
    agent any
   
    stages {
        stage('Create  directory for the WEB Application')
        {
            steps{
               
                //Fisrt, drop the directory if exists
                sh 'rm -rf "$WORKSPACE/tomcat-web"'
                // sh 'rm -rf /home/jenkins/tomcat-web'
                //Create the directory
                sh 'mkdir "$WORKSPACE/tomcat-web"'
                
            }
        }
        stage('Drop the Apache Tomcat Docker container'){
            steps {
            echo 'droping the container...'
            sh 'docker rm -f tomcat1'
            }
        }
        stage('Create the Tomcat container') {
            steps {
            echo 'Creating the container...'
            sh 'docker run -dit --name tomcat1 -p 9090:8080  -v "$WORKSPACE/tomcat-web:/usr/local/tomcat/webapps" tomcat:9.0'
            }
        }
        stage('Copy the web application to the container directory') {
            steps {
                echo 'Creating the shopping folder in the container'
                sh 'mkdir "$WORKSPACE/tomcat-web/shopping"'
                echo 'Copying web application...'             
                sh 'cp -r shopping/* "$WORKSPACE/tomcat-web/shopping"'
            }
        }
    }

    post {
        success {
        // One or more steps need to be included within each condition's block.
        echo 'the deployment has worked'
       }
       failure {
        // One or more steps need to be included within each condition's block.
        echo 'An error has ocurred'
      }
 }
}
