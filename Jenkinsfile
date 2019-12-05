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
    stage ('Test') {
      steps {
        sh 'echo "Run first test!!"'
	sh 'echo "Run second test!!"'
	sh 'echo "Run third test!!"'
	sh 'echo "Run last test!!"'
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
