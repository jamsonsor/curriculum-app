pipeline {
  agent any
  stages {
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/jamsonsor/curriculum-app', branch: 'dev')
      }
    }

    stage('Log') {
      steps {
        sh 'ls -la'
      }
    }

    stage('Build') {
      steps {
        sh 'docker build -f curriculum-front/Dockerfile -t jamson93/curriculum-front:latest .'
        sh 'docker build -f curriculum-back/Dockerfile -t jamson93/curriculum-back:latest .'
      }
    }

    stage('Log into Dockerhub') {
      environment {
        DOCKERHUB_USER = 'jamson93'
        DOCKERHUB_PASSWORD = credentials('DOCKERHUB_PASSWORD')
      }
      steps {
        sh 'docker login -u $DOCKERHUB_USER -p $DOCKERHUB_PASSWORD'
      }
    }

    stage('Push') {
      steps {
        sh 'docker push jamson93/curriculum-front:latest'
        sh 'docker push jamson93/curriculum-back:latest'
      }
    }

  }
}