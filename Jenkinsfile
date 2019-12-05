pipeline {
  environment {
    registry = "anuraagrijal/hello-world-jenkins"
    registryCredential = 'dockerhub'
  }
  agent any
  stages {
    stage('Docker Build') {
      steps {
        sh "docker build --network dcf236262ec0 -t anuraagrijal/hello-world-jenkins-dev:${env.BUILD_NUMBER} ."
      }
    }
    stage('Docker Push') {
      steps {
          sh "docker push anuraagrijal/hello-world-jenkins-dev:${env.BUILD_NUMBER}"
        }
      }
    stage('Docker Remove Image') {
      steps {
        sh "docker rmi anuraagrijal/hello-world-jenkins-dev:${env.BUILD_NUMBER}"
      }
    }
    stage('Run Tests') {
      parallel {
        stage('Test On Chrome') {
          steps {
            echo 'Running test on Chrome!!'
          }
          post {
            success {
              echo 'SUCCESS'
            }
          }
        }
	stage('Test On Firefox') {
          steps {
            echo 'Running test on Firefox!!'
          }
          post {
            success {
              echo 'SUCCESS'
            }
          }
        }
	stage('Test On IE') {
          steps {
            echo 'Running test on IE!!'
          }
          post {
            success {
              echo 'SUCCESS'
            }
          }
        }
      }
    }
/*
    stage('Apply Kubernetes Files') {
      steps {
          withKubeConfig([credentialsId: 'kubeconfig']) {
          sh 'cat deployment.yaml | sed "s/{{BUILD_NUMBER}}/$BUILD_NUMBER/g" | kubectl apply -f -'
          sh 'kubectl apply -f service.yaml'
        }
      }
  }
*/
}
post {
    success {
      echo "Success!!!"
    }
    failure {
      echo "Pipeline failed. Please check the logs."
    }
}
}
