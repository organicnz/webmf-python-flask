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
        if (!fileExists('.env')){
            echo 'Creating virtualenv ...'
            sh 'virtualenv --no-site-packages .env'
        fi
        . .env/bin/activate
        if [[ -f requirements/preinstall.txt ]]; then
            pip install -r requirements/preinstall.txt
        fi
        pip install -r requirements/test.txt
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