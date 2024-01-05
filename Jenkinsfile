@Library("jhc-libs") _

pipeline {
    agent any


stages {
    
stage('maven build') {
            steps {
                sh 'mvn clean package'
            }
        }
       stage('tomcat deploy') {
            steps {
            
            tomcatDeploy('172.31.32.232','ec2-user','tomcat-dev','doctor-online.war')
       
            }
        }
        
        
    }

    
    post {
      success {
        cleanWs()
      }
    }
}
