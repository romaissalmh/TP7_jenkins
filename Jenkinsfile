pipeline {
  agent any
  stages {
    stage('build') {
      post {
        success {
          archiveArtifacts 'build/libs/*.jar'
          junit 'build/reports/tests/test/*.xml'
        }

      }
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
      }
    }

  }
}