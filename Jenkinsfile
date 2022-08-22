pipeline {
    agent any
    environment {
        PATH = "/opt/maven/bin:$PATH"
    }
    stages {
        stage("clone code from git"){
            steps{
                git 'https://github.com/ravdy/hello-world.git'
            }
        }    
        stage("build code"){
            steps{
              sh "mvn clean install"
            }
        }    
        stage("deploy"){
            steps{
              sshagent(['deploy_user']) {
                sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/pipeline/webapp/target/webapp.war ec2-user@18.191.215.240:/opt/tomcat/apache-tomcat-8.5.82/webapps"
                }
            }
        }
    }
}
