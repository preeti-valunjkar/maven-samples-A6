pipeline {
  agent any
  tools { 
      maven 'DHT_MVN' 
      jdk 'DHT_SENSE' 
  }
  stages {
    stage('check out') {
      steps {
        cleanWs()
        git(url: 'https://github.com/dhetong/maven-samples-A6.git', branch: 'master')
      }
    }

    stage('test') {
      steps {
        sh 'mvn clean test'
      }
      post {
        failure {
          sh 'echo "hello"'
        }
      }
    }

  }
}
