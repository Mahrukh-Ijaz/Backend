pipeline {
  environment {
    registry = "mahrukhijaz/backend"
    registryCredential = 'docker-creds'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/mahrukhijaz/backend.git'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":latest"
        }
      }
    }

    stage('Test Code' ) {
            steps {
                sh 'docker container run -p 9090:8080 --name backendNode -d mahrukhijaz/backend:latest'
                sh 'curl -I http://0.0.0.0:9090'
            }
        }


    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    
  }
}
