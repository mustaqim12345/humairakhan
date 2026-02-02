pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }

    stage('Docker Build') {
      steps {
        sh 'docker build -t java-app:latest .'
      }
    }

    stage('Docker Run') {
      steps {
        sh '''
          docker rm -f java-app-container || true
          docker run -d --name java-app-container -p 8080:8080 java-app:latest
        '''
      }
    }

    stage('Deploy') {
      steps {
        sh 'ansible-playbook deploy.yml'
      }
    }
  }
}




