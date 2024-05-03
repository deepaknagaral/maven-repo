pipeline {
    // add your slave label name
    agent { label 'slave'}
    tools{
        maven 'maven-tool-config'
    }
    stages {
        stage ('cloning') {

            steps {
          	    
	     checkout scm
            }
        }

        stage ('build') {

            steps {
               sh 'mvn clean package'
            }
        }
        
        stage ('deployment') {

            steps {
	      sshagent(['tomee']) {
              sh "scp -o StrictHostKeyChecking=no  target/maven-web-application.war  ec2-user@172.31.32.114:/opt/tomcat9/webapps"
	      }
         }
        }
        
    }
}
