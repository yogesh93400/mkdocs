pipeline {
  environment {
    registry = "yogesh93/calculatorproject"
    registryCredential = 'dockerhub_id'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/yogesh93400/mkdocs'
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
