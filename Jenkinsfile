#!groovy

pipeline {
  agent none

  options {
    ansiColor('xterm')
    timestamps()
  }

  stages {
    stage('Build and scan') {
      agent { label 'ecs-builder-node14' }
      steps {
        script {
          initBuild()
          sh 'npm install'
          securityScan()
          sh 'npm test'

          if (env.BRANCH_NAME == '1.3') {
            publishNewNpmVersionIfAny("./package.json", ".")
          }
        }
      }
    }
  }
}