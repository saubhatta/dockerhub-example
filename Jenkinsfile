pipeline {
  agent {
      docker {
            image 'docker:26.0.0-dind'
            args '--privileged -v /var/lib/docker' // Required for DinD
        }
    }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    DOCKER_TLS_CERTDIR = ''
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
