pipeline {
  agent any
  stages {
    stage('Clone repository') {
      steps {
        checkout scm
      }
    }

    stage('Build image') {
      steps {
        script {
          def app = docker.build("hydrangea19/kiii_4")
        }

      }
    }

    stage('Push image') {
      steps {
        script {
          docker.withRegistry("$DOCKER_REGISTRY", 'dockerhub') {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
            // signal the orchestrator that there is a new version
          }
        }

      }
    }

  }
  environment {
    DOCKER_REGISTRY = 'https://registry.hub.docker.com'
  }
}