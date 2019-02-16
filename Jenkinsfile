pipeline {
  agent { label 'windows' }
  options {
    timestamps()
    disableConcurrentBuilds()
    buildDiscarder(logRotator(numToKeepStr: '30'))
  }
  parameters {
      string(name: 'SERVICE_NAME',  defaultValue: '', description: 'Service Name, eg. BsuinessIntelligence')
      string(name: 'SERVICE_PORT',  defaultValue: '', description: 'Servie Port Number, eg. 5000')
      string(name: 'SLACK_CHANNEL', defaultValue: '#infralogs', description: 'Slack channel to publish build message')
  }

  stages {
    stage('dependencies') {
      steps {
         script {
          bat 'dotnet restore'
        }
      }
    }
    stage('build'){
      steps {
        script {
          bat 'dotnet build --configuration Release'
        }
      }
    }
    stage('publish') {
      steps {
        script {
          bat 'dotnet publish --configuration Release --output .\\bin\\Publish'
          bat 'del .\\bin\\Publish\\*.pdb'
        }
      }
    }
    stage('host') {
      steps {
        script {
          bat 'echo publicando no IIS'
        }
      }
    }
  }

  // post {
  //   always {
  //     deleteDir()
  //     //sendNotifications slack_channel: SLACK_CHANNEL
  //   }
  // }
}