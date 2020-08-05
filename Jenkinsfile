pipeline {
  agent { docker { image 'python:3.7.6' } }
  stages {
    stage('build') {
      steps('Make Virtual Env') {
        // withEnv(["HOME=${env.WORKSPACE}"]) {
        //     sh '. .env/bin/activate'
        //     sh 'pip3 install -r requirements.txt --user'
        // }
        withPythonEnv('Python3') {
            sh 'pip install -r requirements.txt --user'
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