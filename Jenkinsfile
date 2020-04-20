pipeline {

  agent any
  tools { maven 'Maven' }
  
  stages {
    
    stage ('Initialize')  { steps { sh 'pwd' 
                                   sh 'whoami'  } }                                     
    
    stage ('Check-Git-Secrets') { steps {
                                            sh 'rm trufflehog || true'
                                            sh 'docker run gesellix/trufflehog --json https://github.com/kdtejas/mavenexample.git > trufflehog'
                                            sh 'cat trufflehog'  } }
    
    stage ('Owasp-Check') { steps { 
                                       sh 'rm owasp* || true'
                                       sh 'wget "https://github.com/kdtejas/mavenexample/blob/master/owasp-check.sh" '
                                       sh 'chmod +x owasp-check.sh'
                                       sh 'bash owasp-check.sh'
                                       sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/owasp-check-report.xml' } } 
    
    stage ('Build')       { steps { sh 'mvn clean package' } }
    
    stage ('Deploy-To-Tomcat') { steps { sh 'cp target/*.war /var/lib/tomcat8/webapps/mavenexample.war' } }
    
              
  } //stages
}
