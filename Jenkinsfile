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
    stage('Running Trigger API Tests') {
      parallel {
        stage('Running Trigger API Tests') {
          agent any
          steps {
            catchError() {
              bat 'npm run trigger-tests'
            }
            
          }
        }
        stage('Running MM API Tests') {
          agent any
          steps {
            catchError() {
              bat 'npm run mm-tests'
            }
            
          }
        }
        stage('FTP API Tests') {
          steps {
            bat 'npm run ftp-tests'
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