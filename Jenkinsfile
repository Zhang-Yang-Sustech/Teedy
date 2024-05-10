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
                // 使用Docker命令构建镜像
                sh "sudo docker build -t ${IMAGE_NAME}:${TAG} -f Dockerfile ."
            }
        }

        stage('Push Image') {
            steps {
                // 登录Docker Hub
                withCredentials([usernamePassword(credentialsId: DOCKER_CREDENTIALS_ID, usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    // 使用Docker命令登录
                    sh "sudo docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"
                    // 使用Docker命令推送镜像
                    sh "sudo docker push ${IMAGE_NAME}:${TAG}"
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
