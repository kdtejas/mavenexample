pipeline {

  agent any
  tools {
    maven 'Maven'
  }
  
  stages {
            stage ('Initialize') {
                                    steps {
                                         sh 'pwd' 
                                    }
            }
            stage ('Build') {
              steps {
              sh 'mvn clean package'
               }
            }
    
  }
}
