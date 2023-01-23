pipeline {
  agent any
  options {
    buildDiscarder(
      logRotator(
        numToKeepStr: '2'
      )
    )
  }
  stages {
    stage('clone down') {
      agent {
        label 'swarm'
      }

      steps {
        stash excludes: '.git/', name: 'code'
      }
    }
    stage('say hello') {
      parallel {
        stage('say hello') {
          steps {
            sh 'echo "Hello World!"'
          }
        }

        stage('build app') {
          agent {
            docker {
              image 'gradle:6-jdk11'
            }

          }
          steps {
            skipDefaultCheckout(true)
            unstash 'code'
            sh 'sh ci/build-app.sh'
            archiveArtifacts 'app/build/libs/'
          }
        }

      }
    }

  }
}