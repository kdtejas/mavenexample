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
	  	stage ('Check-Git-Secrets') { steps {
			 		    sh 'docker pull gesellix/trufflehog'
                                            sh 'rm trufflehog || true'
                                            sh 'docker run gesellix/trufflehog --json https://github.com/kdtejas/mavenexample.git > trufflehog'
                                            sh 'cat trufflehog'  } }
	  
	  	stage ('Deploy-to-tomcat')
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
