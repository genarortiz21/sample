pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3002:3002'
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
	when {
		branch 'production'
	}
      steps {
        input(message: 'Approve?', submitter: 'dev2')
      }
    }
    stage('Deploy to development') {
	when {
		branch 'development'
	}
      steps {
        echo 'Succesful'
      }
    stage('Deploy to production') {
        when {
                branch 'production'
        }
      steps {
        echo 'Succesful'
      }
    }
  }
}
