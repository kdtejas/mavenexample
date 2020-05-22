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
		stage ('Build') { steps { sh 'mvn clean package' } }
	  
	  stage('Deploy-to-tomcat')
	{
		steps
		{
			sshagent(['tomcat'])
			{
				sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@13.232.137.190:/var/lib/tomcat8/webapps/webapp.war'
			}
		}
	}
  }
}
