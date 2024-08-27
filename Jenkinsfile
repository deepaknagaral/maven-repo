pipeline {
    // add your slave label name
    agent { label 'worker'}
    tools{
        maven 'maven_tool_config'
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
              sh "scp -o StrictHostKeyChecking=no  target/maven-web-application.war  ec2-user@43.205.115.22:/opt/tomcat9/webapps"
	      }
         }
        }
        
    }
}
