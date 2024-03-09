pipeline {
    // add your slave label name
    agent { label 'slave1'}
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
	      sshagent(['tomcat-web']) {
              sh "scp -o StrictHostKeyChecking=no  target/maven-web-application.war  ec2-user@16.16.186.187:/opt/tomcat9/webapps"
	      }
         }
        }
        
    }
}
