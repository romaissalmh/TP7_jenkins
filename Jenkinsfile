pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
      }
      post{
      	success { 
      		archiveArtifacts 'build/libs/*.jar'
            junit 'build/test-results/*.xml'
       }
      }
    }

  }
}