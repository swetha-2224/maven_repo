pipeline {
    // add your slave label name
    agent { label 'node-1'}
    tools{
        maven 'maven-test'
    }
    stages {
        stage ('Checkout_SCM') {

            steps {
          	    
	     checkout scm
            }
        }

        stage ('Maven_Build') {

            steps {
               sh 'mvn clean package'
            }
        }
        
        stage ('Deploy_Tomcat') {

            steps {
	      sshagent(['tomcat-server']) {
              sh "scp -o StrictHostKeyChecking=no  target/maven-web-application.war  ec2-user@16.171.194.46:/opt/tomcat9/webapps"
	      }
         }
        }
        
    }
}
