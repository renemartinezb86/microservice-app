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
        sh '''export DOCKER_HOST="tcp://127.0.0.1:2375"
cd microservice
mvn clean
mvn validate
mvn compile
mvn test'''
      }
    }
  }
  tools {
    maven 'Maven 3.5'
    jdk 'JDK 8'
  }
}