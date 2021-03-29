pipeline {
  agent any
  stages {
    stage('build') {
      post {
        success {
          archiveArtifacts 'build/libs/*.jar'
          archiveArtifacts 'build/docs/javadoc/*.xml'
          junit 'build/tests-results/test/*.xml'
        }

      }
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
      }
    }

  }
}