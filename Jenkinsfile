pipeline {
  agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials('srk96-dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh '/usr/local/bin/docker build -t srk96/dp-alpine:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push srk96/dp-alpine:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
