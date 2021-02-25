pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        sh '''
          echo 'Dummy Building ...'
        '''
        script {
          dir('hoge') {
            srcGitRepo = scm.getUserRemoteConfigs()[0].getUrl()
            srcGitBranch =  scm.branches[0].name
            scmVars = checkout(
              [
                $class: 'GitSCM',
                branches: [[name: srcGitBranch]],
                userRemoteConfigs: [[ url: srcGitRepo, ]]
              ]
            )
          }
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
