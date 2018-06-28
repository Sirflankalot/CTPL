pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        parallel {
          "build-clang" : {
            sh 'clang++ -Wall $WORKSPACE/example.cpp -I$WORKSPACE -o $WORKSPACE/example -lpthread'
          }
          "build-gcc" : {
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
