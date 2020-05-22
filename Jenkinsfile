pipeline 
{
  agent any
  tools { maven 'Maven' }
  stages 
  {
		stage ("Start Init") 
		{ 
				steps 
				{ 
					sh 'pwd'
					sh 'whoami'
				}
		}
	  satge('check-git-sevrets'){
	steps
	{
			sh 'docker pull gesellix/trufflehog'
			sh 'rm gitcheck || true'
			sh 'docker run -t gesellix/trufflehog --json https://github.com/kdtejas/mavenexample.git > gitcheck'
			sh 'cat gitcheck'
	}
}
		stage ('Build') { steps { sh 'mvn clean package' } }
	  
	  stage('Deploy-to-tomcat')
	{
		steps
		{
			sshagent(['tomcat'])
			{
				sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@13.233.133.233:/var/lib/tomcat8/webapps/webapp.war'
			}
		}
	}
  }
}
