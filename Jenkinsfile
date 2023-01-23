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
    stage('Say Hello') {
      parallel {
        stage('Say Hello') {
          steps {
            sh 'echo "Hello World!"'
          }
        }

        stage('Build-app') {
          agent {
            docker {
              image 'gradle:6-jdk11'
            }

          }
          steps {
            sh 'sh ci/build-app.sh'
            archiveArtifacts 'app/build/libs/'
          }
        }

      }
    }

  }
}