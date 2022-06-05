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
              sh 'docker login -u AWS -p eyJwYXlsb2FkIjoiRm5iVjZZbmx4Z2FMOTRQcDVVcVZRTDNCbk55dVNjTUdtYUhiNVdxbXI1T0NGNEpxenc4U3RObWpzR1BzcW1wZmxiZ3Fla2tyZnhubzZhdDBvekwva3NTTkZwMEVEMnZOTHphTkE1bFJwdmlYcnNjempYanA3TmduTWlITEI3elR1Yko3aEUzZjNDbmdWbFNRVUxzaVQ2VUVKcTFwd1piSk0xQ1FqNlEvYkQ4a3hOaXBLaHY3WEdxYXVTVFFlUkdESkZkL3EzcDA0SVo0T2xSdUFRTThaVVhzalhrY3RreXRCWm1NelAyN3c0QXBKZWFteTBMQmhnZHJieUpTU2E1ZFVoWE83TDlTbUtUZ1pGbEQzYzBTdVlrRjJBZWwrei9OTEU5TFJ4UXQ2QU9ObVdNMWlpN01KOEdJbnVmMDU4N3FacVhpUVFvS3R5QVg2MmNNdytSTDhjSkp0T2taU3E2UU1FY09aK1JwSm52eFFuU3l0N0lVZ0NNNE44anZEdFpQcnR2TWxoU014Y25URFZVNUhUV1ZYaGQ5ZUduVXFEVDB5T2RBay9nVk5jNkw4U3BIZUpGSjRvTUdweDBQRytSTkxJbDVhUHEvcHBxb0VrQlYzMmVINlNIK2swdmlMMXpGb2w1WGtTdDlBakpac3FFNTFJZXBDYkZKM0lLVG4yZTBzdDlPS0x2dUc4VU9mdlgzVU9DK1VyWWdIK0dKMUh6aUtWeFg3MmI0VTVkSnl6eVBKNFdqZ0RqNS9NdUxVMTZwNHN6KzVZeWJhb0RuYXJMcFBhcWhGNVNLK2hMTWE5Qk44VjVUMk9EZDdIbFhGcG9ONy94Z0JxRWs0QW5XU3FXemRTTVFLejg4dlJYaG94YW5GU2l5amNLaGEvOXBjM3FDWitiZUcwdDF1akRwaDM3bWRnYUIwamlsSTBpSFR6NS8vNXFaR044bGhIeVBoUjNWRnZ6R1NMNW9FaHNlaDlxMzBvQXJBM2NsSUNHSDlGQ3RjekY3alBpUWgzSHNQWkprSUpPaUU1Y3lyeFBQRnppUmJ1QkdCcjlYVmVITXBvU0ZFTjlDa29ZRlYxdUlocXZXMXJacTR1blNManZRWkNQZU9oTHlDdmFjV21ENTJzQmxsMVAzUFR4STMvTWdEZmxOUGVuUEtMZTYyYi96dDNZdGJvYWY0L1FXQSttbmVpMU5uR1NDOVRiR2R4MFcrdXZ1YUlDNnhuR3MxQmViUlppS0xPc3lxUWFPRmtJazJBaVNYbkJlbmFhLzFLWFFxQVVBTnhKQkpqNmRqOUFQZXdsbWNFQUd0bzhNUkVtbm1MSnFKSE5BTWNUeEoyYVNWWVVPUjl2amQ3cnhBc2RIOVNEYWFLb0pkZFNER1h1U2oweVFtNjVjVXZRNWpsTnhOS1NocWc9PSIsImRhdGFrZXkiOiJBUUVCQUhoK2RTK0JsTnUwTnhuWHdvd2JJTHMxMTV5amQrTE5BWmhCTFpzdW5PeGszQUFBQUg0d2ZBWUpLb1pJaHZjTkFRY0dvRzh3YlFJQkFEQm9CZ2txaGtpRzl3MEJCd0V3SGdZSllJWklBV1VEQkFFdU1CRUVERGRucDZKbS81TEVGaHpwQVFJQkVJQTd0T0x4Z3JNK1I3OWhlWWFCNm84N1p3Tk80RElqbzhkOUREcmk3MkV4T1lGcEp5dWpzWXptUENuMVFDYVJJWi9mT0ZzWEZ5M2Z4clcwRVEwPSIsInZlcnNpb24iOiIyIiwidHlwZSI6IkRBVEFfS0VZIiwiZXhwaXJhdGlvbiI6MTY1NDQ5NTg2MH0= https://190274974994.dkr.ecr.eu-west-1.amazonaws.com'
                docker.withRegistry('http://190274974994.dkr.ecr.eu-west-1.amazonaws.com/flask-blog', 'ecr:eu-west-1:AWS-ECR') {
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