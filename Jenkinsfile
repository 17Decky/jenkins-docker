pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t decky17/jenkins-docker-hub .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo  | docker login -u  --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push decky17/jenkins-docker-hub'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
