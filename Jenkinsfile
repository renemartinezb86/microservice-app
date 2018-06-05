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
        sh '''export JAVA_HOME=/usr/lib/jvm/java-1.8.0
export M2_HOME=/usr/local/apache-maven-3.5.3
echo $M2_HOME
export PATH=${M2_HOME}/bin:${PATH}
mvn --version'''
        echo 'Maven build'
        sh '''cd microservice
mvn clean
mvn package'''
      }
    }
  }
}