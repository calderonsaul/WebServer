pipeline {
  agent any
  stages {
    stage('content') {
      parallel {
        stage('content') {
          steps {
            sh 'ls -ltr'
          }
        }

        stage('version') {
          steps {
            sh 'git --version'
          }
        }

      }
    }

    stage('message') {
      steps {
        echo 'Starting CI'
      }
    }

    stage('image') {
      steps {
        sh 'docker build -t calderonsaul/webserver:vy .'
      }
    }

    stage('container') {
      steps {
        sh 'docker run -d --name WebServerCI -p 55:80 webserver:vy'
      }
    }

    stage('status') {
      parallel {
        stage('status') {
          steps {
            echo 'checking status'
          }
        }

        stage('image') {
          steps {
            sh 'docker images'
          }
        }

        stage('container') {
          steps {
            sh 'docker ps'
          }
        }

      }
    }

    stage('message2') {
      steps {
        echo 'complete'
      }
    }

  }
}