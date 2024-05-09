pipeline {
  agent any
  stages{
    // Building Docker images
    stage('Building image') {
      steps{
        sh 'docker build -t teedy2024_manual .'

      }
    }
    // Uploading Docker images into Docker Hub
    stage('Upload image') {
      steps{
        sh 'docker tag teedy2024_manual 3055481367sustech/teedytest2024:v1.0'
        sh 'docker push 3055481367sustech/teedytest2024:v1.0'
      }
    }
    //Running Docker container
    stage('Run containers'){
      steps{
        sh 'docker run -d -p 8084:8080 --name teedy_manual01 teedy2024_manual'
        sh 'docker run -d -p 8082:8080 --name teedy_manual02 teedy2024_manual'
        sh 'docker run -d -p 8083:8080 --name teedy_manual03 teedy2024_manual'

      
      }
    }
  }
}
