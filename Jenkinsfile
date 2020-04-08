pipeline {
  environment {
    registry = "aktechthoughts/simplilearn-devops-certification"
    registryCredential = 'dockerhub'
  }
  agent any
  stages {
        stage('Building image') {
        steps{
            script {
            dockerImage = docker.build registry + ":$BUILD_NUMBER"
            }
        }
        }

        stage('Deploy Image') {
        steps{
            script {
            docker.withRegistry( '', 'dockerhub' ) {
                dockerImage.push()
            }
            }
        }
        }

        stage('Remove Image') {
        steps{
            sh "docker rmi $registry:$BUILD_NUMBER"
        }
        }

        stage('Execute Image') {
        steps{
            imageName = registry + ":$BUILD_NUMBER"
        }
        }
         
    }   
}