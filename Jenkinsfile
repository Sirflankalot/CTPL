pipeline {
  agent any
  stages {
    stage('Build') {
      parallel {
        stage('Build-Clang') {
          steps {
            sh 'clang++ -Wall $WORKSPACE/example.cpp -I$WORKSPACE -o $WORKSPACE/example -lpthread'
          }
        }
        stage('Build-GCC') {
          steps {
            sh 'g++ -Wall $WORKSPACE/example.cpp -I$WORKSPACE -o $WORKSPACE/example -lpthread'
          }
        }
      }
    }
    stage('Execute') {
      steps {
        sh '$WORKSPACE/example'
      }
    }
  }
}