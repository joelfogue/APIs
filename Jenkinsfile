pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/Joel-fogue/APIs.git', branch: 'master')
      }
    }
    stage('Checking Newman\'s Installed') {
      steps {
        bat 'dir'
        bat 'if exist newman_reports cd newman_reports && dir'
        bat 'newman --version'
      }
    }
  }
}