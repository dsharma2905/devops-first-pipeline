pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build Docker') {
      steps {
        script {
          // declare local variable to avoid pipeline warnings
          def dockerImage = docker.build("devanshu/devops-first-pipeline:${env.BUILD_ID}")
          // expose the image name to the next stage
          env.BUILD_DOCKER_IMAGE = "devanshu/devops-first-pipeline:${env.BUILD_ID}"
        }
      }
    }

    stage('Run tests (inside image)') {
      steps {
        script {
          // run commands inside the built image in a temporary container
          docker.image(env.BUILD_DOCKER_IMAGE).inside {
            sh 'python3 -m pip install -r requirements.txt'
            sh 'python3 -c "import flask; print(\\"flask import OK\\")"'
          }
        }
      }
    }
  }

  post {
    always {
      echo "Build ${env.BUILD_ID} finished"
    }
  }
}
