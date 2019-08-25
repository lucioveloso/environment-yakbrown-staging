pipeline {
  options {
    disableConcurrentBuilds()
  }
  agent {
    kubernetes {
      defaultContainer 'jnlp'
      containerTemplate {
        name 'test-a'
        image 'alpine/helm:2.14.0'
        ttyEnabled true
        command 'cat'
      }
    }
  }
  stages {
    stage('Run test') {
      steps {
        container('test-a') {
          sh 'helm init --wait --tiller-namespace pipeline'
          sh 'helm ls --tiller-namespace pipeline' 
        }
      }
    }
  }
}
