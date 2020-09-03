
node {
   // This is to demo github action	
   def sonarUrl = 'sonar.host.url=http://34.215.1.164:9000'
   def mvn = tool (name: 'maven', type: 'maven') + '/bin/mvn'
   stage('SCM Checkout'){
    // Clone repo
	git branch: 'master', 
	credentialsId: 'git',
	git url: 'https://github.com/Alekyagit/my-app'
   
   }
   
   stage('Sonar Publish'){
	   withCredentials([string(variable: 'sonarToken')]) {
        def sonarToken = "sonar.login=${sonarToken}"
        sh "${mvn} sonar:sonar -D${sonarUrl}  -D${sonarToken}"
	 }
      
   }
   
	
   stage('Mvn Package'){
	   // Build using maven 
	   sh "${mvn} clean package deploy"
   }
   
   stage('Email Notification'){
		mail bcc: '', body: """Hi Team, You build successfully deployed
		                       Job URL : ${env.JOB_URL}
							   Job Name: ${env.JOB_NAME}

Thanks,
DevOps Team""", cc: '', from: '', replyTo: '', subject: "${env.JOB_NAME} Success", to: 'alekyajune19@gmail.com'
   
   }
}

