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
        withSonarQubeEnv('sonar') {
          bat 'gradle sonarqube'
        }

        waitForQualityGate true
      }
    }

    stage('Test reporting') {
      steps {
        cucumber '**/cucumber.json'
      }
    }

    stage('Deployment') {
      steps {
        bat 'gradle publish'
      }
    }

    stage('Slack Notification') {
      steps {
        slackSend(message: 'Project is built newly and deployed', channel: '#deployment', baseUrl: 'https://hooks.slack.com/services/', token: 'TC8UCL05R/B01SN4V9S4B/o7VWb53Oaf54K59R6O5nMp79')
      }
    }

  }
}