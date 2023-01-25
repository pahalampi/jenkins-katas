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
          steps {
            sh 'touch something.txt'
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