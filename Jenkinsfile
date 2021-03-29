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

    stage('Mail Notification') {
      steps {
        mail(subject: 'Build status', body: 'Le build a été exécuté.', cc: 'hr_kessi@esi.dz')
      }
    }

  }
}