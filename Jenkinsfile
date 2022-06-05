pipeline {
  environment {
    imagename = "sivin79/my_flask_app"
    //registryCredential = "sivin79"
    registry = '190274974994.dkr.ecr.eu-west-1.amazonaws.com/flask-blog'
    registryCredential = 'aws-cred'
    tag = "latest"
    dockerImage = ''
  }
  agent { label 'flask' }
  stages {
    stage('Building image') {
      steps{
        script {
          dockerImage = sudo docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy image') {
        steps{
            script{
                docker.withRegistry("https://" + registry, "ecr:eu-west-1:" + registryCredential) {
                    sudo dockerImage.push()
                }
            }
        }
    }
  }
}


/*
  agent { label 'flask' }
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/sivin79/my_flask_app.git', branch: 'main', credentialsId: 'dockerhub_sivenkov'])
      }
    }
    stage('Building image') {
      steps{        
        echo "========== Building image ==========="
        sh "docker -v"               
        sh "sudo docker build -t $imagename:$tag ."
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
            sh "sudo docker push $imagename:$tag"
        }
    }
    stage('Remove Unused docker image') {
      steps{
          echo '========== Removing Unused docker image ==========='          
          sh "sudo docker rmi $imagename:$tag"
          sh "curl --version"
          
          withCredentials([string(credentialsId: 'TELEGRAM_TOKEN', variable: 'TELEGRAM_TOKEN'), string(credentialsId: 'TELEGRAM_CHAT_ID', variable: 'TELEGRAM_CHAT_ID')]) {
          sh 'curl -s -X POST https://api.telegram.org/bot$TELEGRAM_TOKEN/sendMessage -d chat_id=$TELEGRAM_CHAT_ID -d text="CI finished success!"'
          }
      }
    }
  }
}
*/