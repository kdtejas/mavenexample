pipeline 
{
  agent any
  tools { maven 'Maven' }
  stages 
  {
		stage ("Start Init") 
		{ steps { 	sh 'pwd' 
			 	sh 'whoami' }
		}
		stage ('Build') { steps { sh 'mvn clean package' } }
		stage ('SAST') { steps {
			withSonarQubeEnv('sonar') {
				sh 'mvn sonar:sonar'
				//sh 'cat target/sonar/report-task.txt' 
			} }
		}
	  stage ('Source-compostion-analysis') 
		{
			steps
			{
				sh 'rm owasp* || true'
				sh 'wget https://raw.githubusercontent.com/kdtejas/mavenexample/master/owasp-check.sh'
				sh 'chmod +x owasp-check.sh'
				sh './owasp-check.sh'		
			}
		}
	  	stage ('Check-Git-Secrets') { steps {
			 		    sh 'docker pull gesellix/trufflehog'
                                            sh 'rm trufflehog || true'
                                            sh 'docker run gesellix/trufflehog --json https://github.com/kdtejas/mavenexample.git > trufflehog'
                                            sh 'cat trufflehog'  } }
	  
		stage ('DAST')
		{ steps { /*sshagent(['zap-ssh']) {
				sh 'ssh -o StrictHostKeyChecking=no ubuntu@234.78.4.21 "docker run -t owasp/zap2docker-stable zap-baseline.py -t http://89.34.204.21:8080/webapp" || true'
			} */ } 
		}
	  
	  	stage ('Deploy-to-tomcat')
		{
			steps
			{
			sshagent(['tomcat'])
			{
				sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@13.233.15.162:/var/lib/tomcat8/webapps/webapp.war'
			}
			}
		}
  }
}
