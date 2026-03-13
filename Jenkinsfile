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
          dockerImage = docker.build("devanshu2905/devops-first-pipeline:${env.BUILD_NUMBER}")
        }
      }
    }

    stage('Push to Docker Hub') {
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-creds') {
            dockerImage.push()
          }
        }
      }
    }

    stage('Run tests (inside image)') {
      steps {
        script {
          docker.withRegistry('', '') {  // no login needed here
            dockerImage.inside {
              sh """
                python3 -m pip install -r requirements.txt
                python3 -c "import flask; print('flask OK')"    
              """
            }
          }
        }
      }
    }
  }

  post {
    always {
      echo "Build ${env.BUILD_NUMBER} finished"
    }
  }
}
