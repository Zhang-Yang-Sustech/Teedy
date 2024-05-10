pipeline {
  agent any

    environment {
        // 你的Docker仓库的凭证ID
        DOCKER_CREDENTIALS_ID = 'a'
        // 你想要推送的镜像名字
        IMAGE_NAME = 'teedytest2024'
        // 你想要推送的Docker Hub用户名
        DOCKER_HUB_USER = '3055481367sustech'
        // 标签，可以根据实际情况设置
        TAG = 'v1.0'
    }

  stages{
    stage('Package') {
      steps {
        checkout scm
        sh 'mvn -B -DskipTests clean package'
      }
    }
    
    // Building Docker images
    stage('Building and push image') {
      steps{
        script {
            // 登录Docker Hub
            docker.withRegistry('https://registry.hub.docker.com', DOCKER_CREDENTIALS_ID) {
                // 使用仓库中的Dockerfile构建镜像
                def customImage = docker.build("${DOCKER_HUB_USER}/${IMAGE_NAME}:${TAG}", '-f Dockerfile .')
                // 推送标签
                customImage.push()
            }
        }
      }
    }
    // // Uploading Docker images into Docker Hub
    // stage('Upload image') {
    //   steps{
    //     sh 'sudo docker tag teedy2024_manual 3055481367sustech/teedytest2024:v1.0'
    //     sh 'sudo docker push 3055481367sustech/teedytest2024:v1.0'
    //   }
    // }
    //Running Docker container
    stage('Run containers'){
      steps{
        sh 'sudo docker run -d -p 8084:8080 --name teedy_manual01 ${IMAGE_NAME}:${TAG}'
        sh 'sudo docker run -d -p 8082:8080 --name teedy_manual02 ${IMAGE_NAME}:${TAG}'
        sh 'sudo docker run -d -p 8083:8080 --name teedy_manual03 ${IMAGE_NAME}:${TAG}'

      
      }
    }
  }
}
