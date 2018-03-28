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
    stage('Clean') {
      steps {
        bat 'if exist newman_reports rd /s /q newman_reports'
      }
    }
    stage('RUNNING API TESTS') {
      parallel {
        stage('FTP API Tests') {
          steps {
            bat 'npm run ftp-tests'
          }
        }
        stage('MM API TESTS') {
          steps {
            bat 'npm run mm-tests'
          }
        }
         stage('TRIGGER API TESTS') {
          steps {
            bat 'npm run trigger-tests'
          }
        }
      }
    }
    stage('Reporting Tests Results') {
      steps {
        junit 'newman_reports/newman.xml'
      }
    }
  }
}
