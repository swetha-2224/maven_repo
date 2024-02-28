pipeline {
    // add your slave label name
    agent { label 'jen-slave-worker1'}
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
              sh "scp -o StrictHostKeyChecking=no  target/maven-web-application.war  ec2-user@13.50.238.247:/opt/tomcat9/webapps"
	      }
         }
        }
        
    }
}
