pipeline {
  agent { docker { image 'python:3.7.6' } }
  stages {
    stage('build') {
      steps('Make Virtual Env') {
        withEnv(["HOME=${env.WORKSPACE}"]) {
            echo "${env.WORKSPACE}"
            sh 'pip3 install -r requirements.txt --user'
        }
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