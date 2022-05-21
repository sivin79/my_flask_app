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
        git([url: 'https://github.com/sivin79/my_flask_app.git', branch: 'main', credentialsId: 'dockerhub_sivenkov'])

      }
    }
    stage('Building image') {
      steps{        
        sh 'docker -v'
        sh 'echo $dockerhub_sivenkov'        
        sh 'sudo docker build -t $imagename .'
      }
    }
    stage('Docker login') {
        steps {
            sh "echo '==========docker login==========='"
            withCredentials([usernamePassword(credentialsId: 'dockerhub_sivenkov', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh 'docker login -u $USERNAME -p $PASSWORD'
            }
        }
    }
    stage('Docker push') {
        steps {
            sh "echo '========== start pushing image ==========='"
            sh 'docker push $imagename:latest'
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