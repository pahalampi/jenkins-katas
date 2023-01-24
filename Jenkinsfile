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
        stage('build app') {
          agent {
              docker {
              image 'gradle:6-jdk11'
            }
          }

          options {
            skipDefaultCheckout(true)
          }

          steps {
            unstash 'code'
            // sh 'ci/build-app.sh'
            // archiveArtifacts 'app/build/libs/'
          }
        }

        stage('test app') {
          agent {
              docker {
              image 'gradle:6-jdk11'
            }
          }

          options {
            skipDefaultCheckout(true)
          }

          steps {
            unstash 'code'
            sh 'ci/build-app.sh'

            sh 'ci/unit-test-app.sh'
            junit 'app/build/test-results/test/TEST-*.xml'
          }
        }
      }
    }
  }

  post {
    cleanup {
      deleteDir()
    }
  }
}