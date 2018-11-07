pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
      args '-u 0:0'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }
    stage('Test') {
      environment {
        CI = 'true'
      }
      steps {
        sh './scripts/test.sh'
      }
    }
    stage('Deliver') {
      steps {
        sh './scripts/deliver.sh'
        input 'Finished using the web site? (Click "Proceed" to continue)'
        sh './scripts/kill.sh'
      }
    }
  }
}
