// pipeline {
//   agent any
//   stages {
//     stage('Build') {
//       steps {
//         sh 'mvn -B -DskipTests clean package'
//       }
//     }
//     stage('Test') {
//       steps {
//         sh 'mvn test --fail-never'
//       }
//     }
//     stage('doc') {
//       steps {
//         sh 'mvn javadoc:javadoc --fail-never'
//       }
//     }
//     stage('pmd') {
//       steps {
//         sh 'mvn pmd:pmd'
//       }
//     }
//     stage('Test report') {
//       steps {
//         sh 'mvn jacoco:report'
//         sh 'mvn surefire-report:report'
//       }
//     }
    
    
    
//   }
//   post {
//       always {
//         archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
//         archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
//         archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
//       }
//   }
// }

pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('K8s') {
            steps {
                sh 'minikube start'
                sh 'kubectl set image deployments/hello-node teedy-my-update-6wq58=3055481367sustech/teedy_my_update:latest'
            }
        }
    }
}
