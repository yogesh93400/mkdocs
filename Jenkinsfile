pipeline {
  environment {
    registry = "yogesh93/calculatorproject"
    registryCredential = 'dockerhub_id'
    dockerImage = ''
  }
  agent any
  stages {
 stage('Clone'){
            steps{
                git credentialsId: '827d70de-0110-405c-9038-5aaf04b08095', url: 'https://git.nagarro.com/freshertraining2021/yogeshyadav01.git'
            }
        }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }

//     stage('Test Mkdocs' ) {
//                 agent {
//                 docker { image 'anishnath/mkdocs:$BUILD_NUMBER' }
//             }
//             steps {
//                 sh 'mkdocs --version'
//             }
//         }


    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}
