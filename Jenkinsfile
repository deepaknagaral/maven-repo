pipeline {
    // add your slave label name
    agent { label 'slave'}
    tools{
        maven 'maven-test'
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
	      sshagent(['My-Tomcat-server']) {
              sh "scp -o StrictHostKeyChecking=no  target/maven-web-application.war  ec2-user@172.31.20.55:/opt/tomcat9/webapps"
	      }
         }
        }
        
    }
}
