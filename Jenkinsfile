@Library('mylibs') _
pipeline{
	/*agent {
		label 'linux'
	}*/
	agent any
	
	 tools {
 		 maven 'maven2'
		}

    stages{
        stage("Git Clone"){
            steps{
                echo "Clone code from git!"
		     // Clone repo
		git branch: 'master', 
		credentialsId: 'github', 
		url: 'https://github.com/javahometech/myweb'
            }
        }
        stage("Maven Build"){
            steps{
                echo "building with maven"
		    sh "mvn clean package"
		     echo "success with maven"
            }
        }
        stage("Tomcat deploy"){
            steps{
		    //credId,username,IpAddrs
                TomcatDeploy("Tomcat-dev","ec2-user","[172.31.85.108]")
            }
        }
    }
}



/*
node {
   // This is to demo github action	
   def sonarUrl = 'sonar.host.url=http://172.31.30.136:9000'
   def mvn = tool (name: 'maven3', type: 'maven') + '/bin/mvn'
   stage('SCM Checkout'){
    // Clone repo
	git branch: 'master', 
	credentialsId: 'github', 
	url: 'https://github.com/javahometech/myweb'
   
   }
   
   stage('Sonar Publish'){
	   withCredentials([string(credentialsId: 'sonarqube', variable: 'sonarToken')]) {
        def sonarToken = "sonar.login=${sonarToken}"
        sh "${mvn} sonar:sonar -D${sonarUrl}  -D${sonarToken}"
	 }
      
   }
   
	
   stage('Mvn Package'){
	   // Build using maven
	   
	   sh "${mvn} clean package deploy"
   }
   
   stage('deploy-dev'){
       def tomcatDevIp = '172.31.28.172'
	   def tomcatHome = '/opt/tomcat8/'
	   def webApps = tomcatHome+'webapps/'
	   def tomcatStart = "${tomcatHome}bin/startup.sh"
	   def tomcatStop = "${tomcatHome}bin/shutdown.sh"
	   
	   sshagent (credentials: ['tomcat-dev']) {
	      sh "scp -o StrictHostKeyChecking=no target/myweb*.war ec2-user@${tomcatDevIp}:${webApps}myweb.war"
          sh "ssh ec2-user@${tomcatDevIp} ${tomcatStop}"
		  sh "ssh ec2-user@${tomcatDevIp} ${tomcatStart}"
       }
   }
   stage('Email Notification'){
		mail bcc: '', body: """Hi Team, You build successfully deployed
		                       Job URL : ${env.JOB_URL}
							   Job Name: ${env.JOB_NAME}

Thanks,
DevOps Team""", cc: '', from: '', replyTo: '', subject: "${env.JOB_NAME} Success", to: 'hari.kammana@gmail.com'
   
   }
}

*/
