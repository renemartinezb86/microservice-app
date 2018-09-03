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
        echo 'Testing ENV'
        sh '''java -version
mvn --version'''
        echo 'Git checkout'
        sh '''pwd
ls'''
        echo 'Maven build'
        sh 'mvn -f microservice-app/pom.xml clean package -Dspring.profiles.active=dev'
      }
    }
    stage('Test') {
      steps {
        echo 'Running test'
        sh '''mvn -f microservice-app/pom.xml test
mvn -f microservice-app/pom.xml gatling:execute
pwd
mv target/gatling/results/*/productgatlingtest*/* target/gatling/results
ls target/gatling/results'''
        junit 'microservice/target/surefire-reports/*.xml'
        script {
          publishHTML(target: [
            allowMissing: false,
            alwaysLinkToLastBuild: false,
            keepAll: true,
            reportDir: 'microservice/target/test-results/coverage/jacoco',
            reportFiles: 'index.html',
            reportTitles: "Coverage Report",
            reportName: "Coverage Report"
          ])
        }

        script {
          publishHTML(target: [
            allowMissing: false,
            alwaysLinkToLastBuild: false,
            keepAll: true,
            reportDir: 'microservice/target/gatling/results',
            reportFiles: 'index.html',
            reportTitles: "Performance Report",
            reportName: "Performance Report"
          ])
        }

      }
    }
    stage('Deploy') {
      steps {
        echo 'Deploy'
      }
    }
  }
  tools {
    maven 'Maven 3.5'
    jdk 'JDK 8'
    git 'Default'
  }
}