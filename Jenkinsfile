pipeline {
  agent { docker { image 'python:3.7.6' } }
  stages {
    stage('build') {
      steps {
        // sh 'virtualenv venv && . venv/bin/activate'
        // sh 'sudo pip install --upgrade pip'
        sh 'whoami 2>/dev/null'
        sh 'pip install -r requirements.txt --user'
      }
    }
    stage('test') {
      steps {
        sh 'python test.py'
      }
      post {
        always {
          junit 'test-reports/*.xml'
        }
      }
    }
  }
}