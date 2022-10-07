pipeline {
  agent any
  stages {
    stage('Pull') {
      steps {
        echo 'Pulling image ...'
        sh 'docker pull ramki007/node-web-app:latest'
      }
    }

    stage('Scan') {
      agent any
      environment {
        LW_ACCESS_TOKEN = '_b71597d2333e350118be296ab87aac2a'
        LW_ACCOUNT_NAME = 'lw100'
      }
      steps {
        echo 'Scanning image ...'
        sh 'curl -L https://github.com/lacework/lacework-vulnerability-scanner/releases/latest/download/lw-scanner-darwin-amd64 -o lw-scanner'
        sh 'chmod +x lw-scanner'
        sh './lw-scanner image evaluate ramki007/node-web-app:latest'
      }
    }

  }
  environment {
    LW_ACCESS_TOKEN = '_b71597d2333e350118be296ab87aac2a'
    LW_ACCOUNT_NAME = 'lw100'
  }
  parameters {
    string(name: 'IMAGE_NAME', description: 'Specify Image Name', defaultValue: '')
    string(name: 'IMAGE_TAG', description: 'Specify Image Tag', defaultValue: '')
  }
}