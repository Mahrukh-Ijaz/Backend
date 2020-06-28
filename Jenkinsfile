pipeline {
  environment {
    registry = "Mahrukh-Ijaz/Backend"
    registryCredential = 'docker-creds'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/Mahrukh-Ijaz/Backend.git'
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
                agent {
                docker { image 'Mahrukh-Ijaz/backend:latest' }
            }
            steps {
                sh 'backend --version'
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
