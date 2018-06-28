pipeline {
  agent none;
  stages {
    stage('Prep') {
      steps {
        node('master') {
          checkout scm;
          stash name: 'source', includes: '*'
          sh 'echo hello world 2'
        }
      }
    }
    stage('Build') {
      parallel {
        stage('Build-Clang') {
          steps {
            node('!master') {
              unstash name: 'source'
              sh 'clang++ -O3 -Wall $WORKSPACE/example.cpp -I$WORKSPACE -o $WORKSPACE/example -lpthread'
              sh '$WORKSPACE/example'
            }
          }
        }
        stage('Build-GCC') {
          steps {
            node('!master')  {
              unstash name: 'source'
              sh 'g++ -O3 -Wall $WORKSPACE/example.cpp -I$WORKSPACE -o $WORKSPACE/example -lpthread'
              sh '$WORKSPACE/example'
            }
          }
        }
      }
    }
  }
}
