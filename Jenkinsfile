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
        sh 'cd microservice'
      }
    }
    stage('Docker') {
      steps {
        sh '''export DOCKER_HOST="tcp://127.0.0.1:2375"
/usr/local/bin/docker-compose --version
cd microservice
docker-compose -f src/main/docker/app.yml up -d
docker commit docker_microservice-app_1 rbravet/microservice
'''
        script {
          docker.withRegistry('https://index.docker.io/v1/', 'docker_rbravet') {
            /* def customImage = docker.build("rbravet/microservice")
            Push the container to the custom Registry
            customImage.push()*/
            sh 'docker tag rbravet/microservice rbravet/microservice'
            sh 'docker push rbravet/microservice'
          }
        }

      }
    }
  }
  tools {
    maven 'Maven 3.5'
    jdk 'JDK 8'
  }
}