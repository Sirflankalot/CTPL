pipeline {
  agent any;
  stages {
    stage('Prep') {
      steps {
        stash name: 'source', includes: '*'
        sh 'echo hello world 2'
      }
    }
    stage('Build') {
      parallel {
        stage('Build-Clang') {
          steps {
            node('gce-worker') {
              unstash name: 'source'
              sh 'clang++ -O3 -Wall $WORKSPACE/example.cpp -I$WORKSPACE -o $WORKSPACE/example -lpthread'
              sh '$WORKSPACE/example'
            }
          }
        }
        stage('Build-GCC') {
          steps {
            node('gce-worker')  {
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
