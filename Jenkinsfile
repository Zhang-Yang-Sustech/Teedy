pipeline {
  agent any
  stages{
    stage('Package') {
      steps {
        checkout scmGit(branches: [[name: '*/b-12110424']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Zhang-Yang-Sustech/Teedy.git']])
        sh 'mvn -B -DskipTests clean package'
      }
    }
    
    // Building Docker images
    stage('Building image') {
      steps{
        sh 'echo "WgV2fMgSyakT~^v" | sudo -S docker build -t teedy2024_manual .'

      }
    }
    // Uploading Docker images into Docker Hub
    stage('Upload image') {
      steps{
        sh 'sudo docker tag teedy2024_manual 3055481367sustech/teedytest2024:v1.0'
        sh 'sudo docker push 3055481367sustech/teedytest2024:v1.0'
      }
    }
    //Running Docker container
    stage('Run containers'){
      steps{
        sh 'sudo docker run -d -p 8084:8080 --name teedy_manual01 teedy2024_manual'
        sh 'sudo docker run -d -p 8082:8080 --name teedy_manual02 teedy2024_manual'
        sh 'sudo docker run -d -p 8083:8080 --name teedy_manual03 teedy2024_manual'

      
      }
    }
  }
}
