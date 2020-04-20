pipeline {

  agent any
  tools { maven 'Maven' }
  
  stages {
    
    stage ('Initialize')  { steps { sh 'pwd'   } }                                     
    stage ('Build')       { steps { sh 'mvn clean package' } }
    stage ('Deploy-To-Tomcat') { steps { sh 'cp target/*.war /var/lib/tomcat8/webapps/mavenexample.war' } }
              
  } //stages
}
