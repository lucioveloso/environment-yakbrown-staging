pipeline {
  options {
    disableConcurrentBuilds()
  }
  agent {
    kubernetes {
      containerTemplate {
        name 'test-a'
        image 'maven:3.3.9-jdk-8-alpine'
        ttyEnabled true
        command 'cat'
      }
    }
  }
  stages {
    stage('Run maven') {
      steps {
        sh 'mvn -version'
        sh "echo Workspace dir is ${pwd()}"
      }
    }
  }
}
