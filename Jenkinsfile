pipeline {
  agent any
  stages {
    stage('Say Hello') {
      parallel {
        stage('Say Hello') {
          steps {
            sh 'echo "Hello World!"'
          }
        }

        stage('Build') {
          agent {
            docker {
              image 'gradle:6-jdk11'
            }

          }
          steps {
            sh 'ci/build-app.sh'
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
  options {
    buildDiscarder(logRotator(numToKeepStr: '2'))
  }
}