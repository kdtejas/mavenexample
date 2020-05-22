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
  }
}
