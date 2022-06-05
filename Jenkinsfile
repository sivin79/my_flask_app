pipeline {
  environment {
    imagename = "sivin79/my_flask_app"
    //registryCredential = "sivin79"
    registry = '190274974994.dkr.ecr.eu-west-1.amazonaws.com/flask-blog'
    registryCredential = 'AWS-ECR'
    tag = "latest"
    dockerImage = ''
  }
  agent { label 'flask' }
  stages {
    stage('Building image') {
      steps{
        script {
          dockerImage = sh "sudo docker build -t $registry:$tag ."
        }
      }
    }
    stage('Deploy image') {
        steps{
            script{
                sh "sudo docker login -u AWS -p eyJwYXlsb2FkIjoiVGhQQ1dBUFdXUjc2Z0cwZ3lsQ2RzVjlrZnovT25NVDJKcUF6aUZZa01aL2FLK2FtSGIzcURRWHAzc3FreGZNT2pZUVNMY2pkaXBQOTFPWSs1bjV1TGVjUUduekRyLzQzQW1wcERSSm1DRVhUOUR0cVo1UU51aU9vRmVxTUhmY21zck5jYWluSmNRZHBaY3cyUnMzemdWZ2hYWCtmZk5pZ0E2L1VMWllMcWVrbitGam9RSUFrUzQvWldrTW0yeFNEMW1DZk5ETDFHazRyWmptZzk4enE2RHBUMUExT2NNZHZWVmg4a1lFVHRsOWYyWGZYZjQ4ZHJLejdQS0s0cC95UWNNQStjOVl1MENqeCtFSWxHQTdtajNKRTlQSXNsSUJMQkFORm9TMG5mVS93NUZDdUlTOXRDZm5wQ2kzdzJIcWFHZFdJQ2k2MkcrVFlwanpDTzZkaWRpNXBicHBwNnRld0x0bmJCcjJPTFUyalZjQXIyQk8yemYzcVVhUUY2SU5GWXV5Z1NESFFVL1JITndVbzVaMmtYeEgrTEgybE41MkpnWWpKUUhLakZFcktpRUJ0a2RGUzJlNEpBazZSTjZ6NUZTNTJyblhwYlVFQ2tMaElhTEhCWnBDRzBOeCtjOHhLTkNtc1JuSG96VzNrc0dKMERobXlGR0NQZXpkakE5cEJ1SUR6Sk5WdVhmZkdzbmh1akxITGZQVUZzdGJ2WFZ2dW5xU3JwdGRlZHUyVGtrN21Od3F0bUU4NTl3NVhFY2QwZEdlNEVDbXNiMm9VWG9lTkpETmd0eTBIU0t6UzJ0LzRDUVRadEVodnVmR2YrSTRxalhCQkp1YWw1WjR5a1d2S0Z0R2tVVkVRQ2h5V29xWEJXNEhiTXRNM0hCcy83R2JETyszNXNEMW01OEFWbE4xV05rOEMxSmtxTXhaaGJEcnlZbENnMDJTZ1Y2TktMWnhZVXBUd09zY3E0NXUyTVgvMU80VFJPQUJCRDBOTktSU3k5ZHl4WTlMQnU4cmlIN3lTOTVuYlVBdEk4OUxvUlRudmpnSDB5c3IrNUFaN2NoTkMxaUtQNCs4dVhFZmp1cDk2N3FkM2wyU25mZ3VnRC9FL3UySzZRcXZydzhmS281T0Z1OEpuclcxcTVISEVhWThIcTc5aC9CZkVUU2dHb2hsa29ic0lNaCtEQlV2M2haUlVmV0hHY09uUGt6MW1zV2xWbjlBWlo1RlNieUFkaUJXQVhBNlQzOVVtN0paeXUxZVpsOVMrTHA5SUx5d0JzRGs1N2I3NE9sTnVTSm1ISktqa1djTHdJRkkwVStyQnQ0TFltb1Nkblcwdy93MmZSclNsYXNTQkhSbWcxS2E1TTJwRy84ZVFjMHZabGdRQ0RBRWZaTG9BU2l2SWhBZzN0SHBmNHc9PSIsImRhdGFrZXkiOiJBUUVCQUhoK2RTK0JsTnUwTnhuWHdvd2JJTHMxMTV5amQrTE5BWmhCTFpzdW5PeGszQUFBQUg0d2ZBWUpLb1pJaHZjTkFRY0dvRzh3YlFJQkFEQm9CZ2txaGtpRzl3MEJCd0V3SGdZSllJWklBV1VEQkFFdU1CRUVES2QvcmRLZHFuZ09NNVlzRVFJQkVJQTdBY1c1RDBUanorNkY2NkYwM04xNm9JN0dJWGpzWmRNMlJwdy9XYU9tNDVZWDFRcUVsVDlyVXJzc0x3UGltMnA1T055aE5oYVVRajBqR0dvPSIsInZlcnNpb24iOiIyIiwidHlwZSI6IkRBVEFfS0VZIiwiZXhwaXJhdGlvbiI6MTY1NDQ5NzUyN30= https://190274974994.dkr.ecr.eu-west-1.amazonaws.com"
                sh "docker push 190274974994.dkr.ecr.eu-west-1.amazonaws.com/flask-blog:latest"
                //docker.withRegistry("http://" + registry, "ecr:eu-west-1:" + registryCredential) {
                //    sudo dockerImage.push()
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