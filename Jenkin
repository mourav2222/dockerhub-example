pipeline {
  agent { label 'linux' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('mourav2222-dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t mourav2222/tank:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push mourav2222/tank:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
} 
