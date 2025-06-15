pipeline {
  agent  none
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub_id')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t saubhatta/from-jenkins:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push saubhatta/from-jenkins:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
