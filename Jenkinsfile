pipeline {
  agent any
  tools { 
      maven 'DHT_MVN' 
      jdk 'DHT_SENSE' 
  }
  environment {
      RUN_BISECT = "false"
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
            env.RUN_BISECT = "true"
        }
      }
    }

    stage('detect first bad commit') {
      when {
        expression { env.RUN_BISECT == "true" }
      }
      steps {
        sh 'git bisect start 198644632661c67b6c32f59e9047c11a70685e15 98ac319c0cff47b4d39a1a7b61b4e195cfa231e5'
        sh 'git bisect run mvn clean test'
      }
    }

  }
}
