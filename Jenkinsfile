pipeline {
  agent any
  stages {
    stage('Build') {
      parallel {
        stage('Build-Clang') {
          steps {
            node {
              sh 'clang++ -O3 -Wall $WORKSPACE/example.cpp -I$WORKSPACE -o $WORKSPACE/example -lpthread'
              sh '$WORKSPACE/example'
            }
          }
        }
        stage('Build-GCC') {
          steps {
            node {
              sh 'g++ -O3 -Wall $WORKSPACE/example.cpp -I$WORKSPACE -o $WORKSPACE/example -lpthread'
              sh '$WORKSPACE/example'
            }
          }
        }
      }
    }
  }
}
