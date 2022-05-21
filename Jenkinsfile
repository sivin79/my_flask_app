pipeline {
  environment {
    imagename = "sivin79/my_flask_app"
    registryCredential = 'sivin79'
    dockerImage = ''
  }
  agent { label 'flask' }
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/sivin79/my_flask_app.git', branch: 'main', credentialsId: '${PAT-01}'])

      }
    }
    stage('Building image') {
      steps{        
        sh 'docker -v'
        sh 'echo ${PAT-01}'
        sh 'sudo docker build -t sivin79/my_flask_app .'
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
             dockerImage.push('latest')

          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $imagename:$BUILD_NUMBER"
         sh "docker rmi $imagename:latest"

      }
    }
  }
}