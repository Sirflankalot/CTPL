pipeline {
  agent {
    label 'master'
  }
  stages {
    stage('Prepare') {
      steps {
        stash name: 'source', includes: '**/*'
      }
    }
    stage('Build') {
      parallel {
        stage('Build-GCC') {
          steps {
            node('gce4-worker') {
              deleteDir()
              unstash name: 'source'
              sh '''g++ -O3 -Wall $WORKSPACE/example.cpp -I$WORKSPACE -o $WORKSPACE/example -lpthread'''
              stash name: 'gcc-build', includes: 'example'
            }
          }
        }
        stage('Build-Clang') {
          steps {
            node('gce4-worker') {
              deleteDir()
              unstash name: 'source'
              sh '''clang++ -O3 -Wall $WORKSPACE/example.cpp -I$WORKSPACE -o $WORKSPACE/example -lpthread'''
              stash name: 'clang-build', includes: 'example'
            }
          }
        }
      }
    }
    stage('Verify') {
      parallel {
        stage('Verify-GCC') {
          steps {
            node('gce8-worker') {
              deleteDir()
              sh 'ls -lah'
              unstash name: 'gcc-build'
              sh 'ls -lah'
              sh '''$WORKSPACE/example'''
            }
          }
        }
        stage('Verify-Clang') {
          steps {
            node('gce8-worker') {
              deleteDir()
              sh 'ls -lah'
              unstash name: 'clang-build'
              sh 'ls -lah'
              sh '''$WORKSPACE/example'''
            }
          }
        }
      }
    }
  }
}
