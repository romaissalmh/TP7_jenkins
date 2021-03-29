pipeline {
  agent any
  stages {
    stage('build') {
      post {
        success {
          archiveArtifacts 'build/libs/*.jar'
          archiveArtifacts 'build/docs/javadoc/*'
          junit 'build/test-results/test/*.xml'
        }

      }
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
      }
    }

  }
}