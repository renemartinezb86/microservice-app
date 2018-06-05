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
        sh '''pwd
cd microservice
mvn clean'''
      }
    }
  }
}