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
          sh 'helm init --client-only'
          sh 'helm repo update'
          sh 'helm plugin install https://github.com/rimusz/helm-tiller'
          sh 'export TILLER_NAMESPACE=PIPELINE'
          sh 'export TILLER_NAMESPACE=$NAMESPACE'
          sh 'export HELM_HOST=127.0.0.1:44134'
          sh 'helm tiller start-ci $NAMESPACE'
          sh 'helm ls' 
        }
      }
    }
  }
}
