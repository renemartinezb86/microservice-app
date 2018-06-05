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
        sh '''java -version
mvn --version
docker --version'''
        echo 'Maven build'
        sh '''cd microservice
mvn clean
mvn package'''
      }
    }
  }
  tools {
    maven 'Maven 3.5'
    jdk 'JDK 8'
  }
}