pipeline {
  agent { docker { image 'python:3.7.6' } }
  stages {
    stage('build') {
      steps {
        // withEnv(["HOME=${env.WORKSPACE}"]) {
        //     sh '. .env/bin/activate'
        //     sh 'pip3 install -r requirements.txt --user'
        // }
        sh """
        if [[!fileExists(.env/bin/activate) ]]; then
            echo 'Creating virtualenv ...'
            sh 'virtualenv --no-site-packages .env'
        fi
        . .env/bin/activate
        if [[ -f requirements.txt ]]; then
            pip install -r requirements.txt
        fi
        pip install -r requirements.txt
        ./manage.py test --noinput
        """
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