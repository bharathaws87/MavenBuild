node(){

	
	stage('Code Checkout'){
		checkout changelog: false, poll: false, scm: scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitHubCreds', url: 'https://github.com/bharathaws87/MavenBuild']])
	}
	stage('Build Automation'){
		sh """
			ls -lart
			mvn clean install
			ls -lart target
		"""
	}
	

	stage('Code Deployment'){
		deploy adapters: [tomcat9(credentialsId: 'TomcatCreds', path: '', url: 'http://13.52.97.175:8080/')], contextPath: 'pipelinetestapp', onFailure: false, war: 'target/*.war'
	}

	stage('email notification'){
		mail bcc: '', body: """<p>SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>""", cc: 'himarshi.m@gmail.com', from: '', replyTo: '', 
		subject: 'Test Application Notification', to: 'bharathaws87@gmail.com'
		
}
}
