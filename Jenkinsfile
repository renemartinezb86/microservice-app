pipeline {
  agent {
    docker {
      image 'rbravet/microservice'
    }

  }
  stages {
    stage('Repo pull') {
      steps {
        git(url: 'https://github.com/renemartinezb86/microservice-app', poll: true)
      }
    }
  }
  environment {
    SPRING_PROFILES_ACTIVE = 'prod,swagger'
    EUREKA_CLIENT_SERVICE_URL_DEFAULTZONE = 'http://admin:${jhipster.registry.password}@jhipster-registry:8761/eureka'
    SPRING_CLOUD_CONFIG_URI = 'http://admin:${jhipster.registry.password}@jhipster-registry:8761/config'
    SPRING_DATA_MONGODB_URI = 'mongodb://microservice-mongodb:27017'
    SPRING_DATA_MONGODB_DATABASE = 'microservice'
    JHIPSTER_SLEEP = '30'
    JHIPSTER_REGISTRY_PASSWORD = 'admin'
    PATH = '/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/lib/jvm/java-1.8-openjdk/jre/bin:/usr/lib/jvm/java-1.8-openjdk/bin'
    LANG = 'C.UTF-8'
    JAVA_HOME = '/usr/lib/jvm/java-1.8-openjdk/jre'
    JAVA_VERSION = '8u151'
    JAVA_ALPINE_VERSION = '8.151.12-r0'
    SPRING_OUTPUT_ANSI_ENABLED = 'ALWAYS'
    JAVA_OPTS = ''
  }
}