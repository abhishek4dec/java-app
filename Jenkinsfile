pipeline{
	agent {
  		label 'linux'
	      }
	tools {
  		maven 'maven2'
        }
	
	stages{
		
	stage("Maven Clean")
		{
			steps{
				sh "mvn clean package"
			}
		}
	}
	stage("Code Deployment"){
		steps{
			sshagent(['tomcat']) {
  					sh "mv target/*.war target/abhishek.war"
					sh "scp target/abhishek.war ec2-user@172.31.1.220:/opt/tomcat9/webapps/"
					sh "ssh ec2-user@172.31.1.220 /opt/tomcat9/bin/shutdown.sh"
					sh "ssh ec2-user@172.31.1.220 /op/tomcat9/bin/startup.sh"
				
				}
		}
	}
	post {
  success {
    echo "this is success"
  }
  failure {
    echo "this is fail"
  }
}

}

/*@Library("app-lib") _
pipeline {
  agent any

  tools {
    maven 'maven3'
  }
  options {
    buildDiscarder logRotator(daysToKeepStr: '10', numToKeepStr: '7')
  }
  parameters {
    choice choices: ['develop', 'qa', 'master'], description: 'Choose the branch to build', name: 'branchName'
  }
  stages {
    stage('Maven Build') {
      steps {
        sh 'mvn clean package'
      }
    }
    stage('Deploy to Tomcat') {
      steps {
        tomcatDeploy(["172.31.13.38","172.31.13.38","172.31.13.38"],"ec2-user","tomcat-dev")
      }
    }
  }
  post {
    success {
      archiveArtifacts artifacts: 'target/*.war'
      cleanWs()
    }
  }
}
*/
