pipeline {
  environment {
    imagename = "sivin79/my_flask_app"
    registryCredential = "sivin79"    
    tag = "latest"
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
    stage('CD') {
        steps {
            echo '========== starting terraform ==========='            
            dir("${env.WORKSPACE}/terraform"){
              sh "pwd" 
              Use Jenkins UsernamePassword credentials information (Username: AccessKeyId, Password: SecretAccessKey):    
              withAWS(credentials:'AWS-CREDS') {
              // do something
              sh "terraform plan"
              }
            }                      
            
        }
    }
  }
}
