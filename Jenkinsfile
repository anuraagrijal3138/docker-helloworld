pipeline {
  agent any
  stages {
    stage('Docker Build') {
      steps {
        sh "docker build -t anuraagrijal/hello-world-jenkins:${env.BUILD_NUMBER} ."
      }
    }
/*
    stage('Docker Push') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'JUi@@11stbest', usernameVariable: 'anuraagrijal')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh "docker push anuraagrijal/hello-world-jenkins:${env.BUILD_NUMBER}"
        }
      }
    }
    stage('Docker Remove Image') {
      steps {
        sh "docker rmi anuraagrijal/hello-world-jenkins:${env.BUILD_NUMBER}"
      }
    }
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
