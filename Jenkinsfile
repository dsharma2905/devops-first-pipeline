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
          dockerImage = docker.build("devanshu/devops-first-pipeline:${env.BUILD_ID}")
        }
      }
    }
    stage('Run tests (smoke)') {
      steps {
        sh 'python3 -m pip install -r requirements.txt'
        sh 'python3 -m pytest -q || true' // no tests yet, placeholder
      }
    }
  }
  post {
    always {
      echo "Build ${env.BUILD_ID} finished"
    }
  }
}
