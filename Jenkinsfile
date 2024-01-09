 @Library("jhc-libs") _

pipeline {
    agent any


stages {
    
stage('maven build') {
            steps {
                sh "mvn clean package"
            }
        }

stage("Upload Artifacts"){
            steps{
              nexusArtifactUploader artifacts: [[artifactId: 'doctor-online', classifier: '', file: 'target/doctor-online.war', type: 'war']], 
                  credentialsId: 'nexus3', 
                  groupId: 'in.javahome',
                  nexusUrl: '172.31.12.199:8081', 
                  nexusVersion: 'nexus3', 
                  protocol: 'http', 
                  repository: 'doctor-release', 
                  version: '1.4'
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
