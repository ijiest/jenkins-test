pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        sh '''
          echo 'Dummy Building ...'
        '''
        print scm.getUserRemoteConfigs()[0].getUrl()
        print scm.branches[0].name
        dir('hoge') {
          sh 'pwd'
        }
      }
    }
    stage('Test') {
      steps {
        echo 'Testing ...'
      }
    }
    stage('Deploy') {
      steps {
        echo 'Deploying ...'
      }
    }
  }
}
