pipeline {
    agent any

    stages {
       
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage("Dev Deploy"){
        steps{
          sshagent(['tomcat-dev']) {
             // copy warfile onto tomcat server
             sh "scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.42.127:/opt/tomcat9/webapps/"
             sh "ssh ec2-user@172.31.42.127 /opt/tomcat9/bin/shutdown.sh"
             sh "ssh ec2-user@172.31.42.127 /opt/tomcat9/bin/startup.sh"
           }  
        }  
      }
    }  
 }  
