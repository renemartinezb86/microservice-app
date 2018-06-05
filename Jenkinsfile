pipeline {
  agent any
  stages {
    stage('Initialize') {
      steps {
        echo 'Initializing pipeline'
      }
    }
    stage('Build') {
      steps {
        echo 'Setting up maven'
        sh '''echo $M2_HOME
export PATH=${M2_HOME}/bin:${PATH}'''
      }
    }
  }
}