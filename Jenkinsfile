pipeline {
  agent any
  stages {
    stage('build') {
      post {
        success {
          archiveArtifacts 'build/libs/*.jar'
          archiveArtifacts 'build/docs/javadocc/*'
          junit 'build/test-results/test/*.xml'
        }

        failure {
          mail(subject: 'Build status', body: "The build has been pushed. The result is: ${currentBuild.currentResult}", to: 'hr_kessi@esi.dz')
        }

      }
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
      }
    }

    stage('Mail Notification') {
      steps {
        mail(subject: 'Build status', body: "The build has been pushed. The result is: ${currentBuild.currentResult}", to: 'hr_kessi@esi.dz')
      }
    }

    stage('Code Analysis') {
      steps {
        waitForQualityGate true
      }
    }

  }
}