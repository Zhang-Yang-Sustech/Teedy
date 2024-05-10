pipeline {
  agent any

    environment {
        // 你的Docker仓库的凭证ID
        DOCKER_CREDENTIALS_ID = 'a'
        // 你想要推送的镜像名字
        IMAGE_NAME = '3055481367sustech/teedytest2024'
        // 标签，可以根据实际情况设置
        TAG = 'v1.0'
    }

  stages{
    stage('Package') {
      steps {
        checkout scm
      }
    }
    
     stage('Build Image') {
            steps {
                script {
                    // 使用仓库中的Dockerfile构建镜像
                    def customImage = docker.build("${IMAGE_NAME}:${TAG}", '-f Dockerfile .')
                }
            }
        }

        stage('Push Image') {
            steps {
                script {
                    // 登录Docker Hub
                    docker.withRegistry('https://registry.hub.docker.com', DOCKER_CREDENTIALS_ID) {
                        // 推送标签
                        customImage.push()
                    }
                }
            }
        }
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
