pipeline {
  agent { docker { image 'python:3.7.6' } }
  stages {
    stage('build') {
      steps {
        withEnv(["HOME=${env.WORKSPACE}"]) {
            sh 'pip3 install -r requirements.txt --user'
            sh '. WORKSPACE/bin/activate'
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