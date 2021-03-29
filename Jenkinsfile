pipeline {
  agent any
  stages {
    stage('build') {
      post {
        success {
          archiveArtifacts 'build/libs/*.jar'
          junit 'build/reports/**/*.xml'
        }

      }
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
      }
    }

  }
}