pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
    }

  }
  stages {
    stage('Install') {
      steps {
        sh 'npm install'
      }
    }
    stage('Build') {
      steps {
        sh 'npm run build'
      }
    }
    stage('Test') {
      steps {
        sh 'npm test'
        emailext(subject: 'Aprobar', body: 'Please Approve', attachLog: true)
      }
    }
    stage('Approve') {
      steps {
        input(message: 'Approve?', submitter: 'dev2')
      }
    }
    stage('Deploy') {
      steps {
        echo 'Succesful'
      }
    }
  }
}
