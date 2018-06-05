pipeline {
  agent any
  stages {
    stage('Initialize') {
      steps {
        echo 'Initializing pipeline'
        git(url: 'https://github.com/renemartinezb86/microservice-app', poll: true, changelog: true, branch: 'master')
      }
    }
    stage('Build') {
      steps {
        sh 'pwd'
      }
    }
  }
}