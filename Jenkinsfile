pipeline {
  agent any
  stages {
    stage('Initialize') {
      steps {
        echo 'Initializing pipeline'
      }
    }
    stage('Build') {
      agent any
      steps {
        echo 'Setting up maven'
        sh 'mvn --version'
        echo 'Maven build'
        sh '''cd microservice
docker --version
mvn clean'''
      }
    }
  }
  tools {
    maven 'Maven 3.5'
    jdk 'JDK 8'
  }
}