pipeline {
  environment {
    imagename = "sivin79/my_flask_app"
    registryCredential = 'sivin79'
    tag = 'v.0.0.2'
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
        echo '========== Building image ==========='
        sh 'docker -v'
        sh 'echo $BUILD_NUMBER'
        sh 'echo $GIT_COMMIT'
        sh 'echo $dockerhub_sivenkov'        
        sh 'sudo docker build -t $imagename:$GIT_COMMIT .'
      }
    }
    stage('Docker login') {
        steps {
            echo '========== docker login ==========='
            withCredentials([usernamePassword(credentialsId: 'dockerhub_sivenkov', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh "sudo docker login -u $USERNAME -p $PASSWORD"
            }
        }
    }
    stage('Docker push') {
        steps {
            echo '========== start pushing image ==========='
            sh "sudo docker push $imagename:$GIT_COMMIT"
        }
    }



    stage('Remove Unused docker image') {
      steps{
          echo '========== Removing Unused docker image ==========='          
          sh "sudo docker rmi $imagename:$GIT_COMMIT"

      }
    }
  }
}