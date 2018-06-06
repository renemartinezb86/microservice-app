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
mvn --version
docker --version'''
        echo 'Maven build'
        sh '''cd microservice
mvn -Pprod clean package'''
      }
    }
    stage('Test') {
      steps {
        echo 'Running test'
        sh '''cd microservice
mvn test
mvn gatling:execute
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
    stage('Sonar') {
      steps {
        echo 'Sonar Test'
        sh '''cd microservice
mvn sonar:sonar \\
  -Dsonar.host.url=http://demo.setit.cl:9002 \\
  -Dsonar.login=bf4e8cd87ffb7ee90e781cf5071c88c80cd927ca'''
        waitForQualityGate true
      }
    }
    stage('Docker') {
      steps {
        sh '''export DOCKER_HOST="tcp://127.0.0.1:2375"
docker ps'''
      }
    }
  }
  tools {
    maven 'Maven 3.5'
    jdk 'JDK 8'
  }
}