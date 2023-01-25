pipeline {
  agent any
  stages {
    stage('Say Hello') {
      steps {
        sh 'echo "Hello World!"'
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