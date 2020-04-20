pipeline {

  agent any
  tools { maven 'Maven' }
  
  stages {
    
    stage ('Initialize')  { steps { sh 'pwd' sh 'whoami' sh 'sudo su' sh 'whoami' } }                                     
    
    stage ('Check-Git-Secrets') { steps {
                                            sh 'rm trufflehog || true'
                                            sh 'docker run gesellix/trufflehog --json https://github.com/cehkunal/webapp.git > trufflehog'
                                            sh 'cat trufflehog'  } }
    
    stage ('Build')       { steps { sh 'mvn clean package' } }
    
    stage ('Deploy-To-Tomcat') { steps { sh 'cp target/*.war /var/lib/tomcat8/webapps/mavenexample.war' } }
    
              
  } //stages
}
