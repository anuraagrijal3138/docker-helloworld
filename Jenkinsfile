pipeline {
  agent any
  stages {
    stage('Docker Build') {
      steps {
        sh "docker build --network dcf236262ec0 -t anuraagrijal/hello-world-jenkins-dev:${env.BUILD_NUMBER} ."
      }
    }

    stage('Run Tests') {
      parallel {
        stage('Test On Chrome') {
          post {
            success {
              echo 'SUCCESS'
            }

          }
          steps {
            sh '''
              sleep 3 
	      echo \'Running test on Chrome!!\'
	    '''
          }
        }

        stage('Test On Firefox') {
          post {
            success {
              echo 'SUCCESS'
            }

          }
          steps {
            sh '''
              sleep 3
	      echo \'Running test on Firefox!!\'
	    '''
          }
        }

        stage('Test On IE') {
          post {
            success {
              echo 'SUCCESS'
            }

          }
          steps {
            sh '''
              sleep 3 
	      echo \'Running test on IE!!\'
	    '''
          }
        }

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
    stage('Apply Kubernetes Deployment') {
      steps {
          sh 'cat deployment.yml | sed "s/'1234512345'/'${env.BUILD_NUMBER}'/g" | kubectl apply -f -'
        }
      }
  }
  environment {
    registry = 'anuraagrijal/hello-world-jenkins-dev'
    registryCredential = 'dockerhub'
  }
  post {
    success {
      echo 'Success!!!'
    }

    failure {
      echo 'Pipeline failed. Please check the logs.'
    }

  }
}
