
def zAppBuildGitRepo   = 'https://github.com/IBM/dbb-zappbuild.git'
def zAppBuildGitBranch = 'development' // Some important issues are not yet merged into master.

pipeline {
  agent any

  stages {
    stage('Git Clone/Refresh') {
      steps {
        script {
          dir("dbb-zappbuild") {
            sh(script: 'rm -f .git/info/sparse-checkout', returnStdout: true)

            def scmVars = checkout([
              $class: 'GitSCM',
              branches: [[name: zAppBuildGitBranch]],
              doGenerateSubmoduleConfigurations: false,
              submoduleCfg: [],
              userRemoteConfigs: [[url: zAppBuildGitRepo,]]
            ])
          }

          /*dir('dbb-zappbuild') {
           *  sh(script: 'rm -f .git/info/sparse-checkout', returnStdout: true)
           *  srcGitRepo = scm.getUserRemoteConfigs()[0].getUrl()
           *  srcGitBranch =  scm.branches[0].name
           *  scmVars = checkout(
           *    [
           *      $class: 'GitSCM',
           *      branches: [[name: srcGitBranch]],
           *      userRemoteConfigs: [[ url: srcGitRepo, ]]
           *    ]
           *  )
           */}
        }
      }
    }
    stage('Publish') {
      steps {
        script {
          sshPublisher(
            publishers: [
              sshPublisherDesc(
                configName: 'e2e-pipeline',
                transfers: [
                  sshTransfer(
                    sourceFiles: "dbb-zappbuild",
                    removePrefix: "",
                    remoteDirectory: '',
                    cleanRemote: false,
                    excludes: '',
                    execCommand: "",
                    execTimeout: 120000,
                    flatten: false,
                    makeEmptyDirs: false,
                    noDefaultExcludes: false,
                    patternSeparator: '[, ]+',
                    remoteDirectorySDF: false,
                  )
                ],
                usePromotionTimestamp: false,
                useWorkspaceInPromotion: false, verbose: false
              )
            ],
            alwaysPublishFromMaster: true
          )
        }
      }
    }
    stage('Build') {
      steps {
        sh '''
          echo 'Dummy Building ...'
        '''
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
