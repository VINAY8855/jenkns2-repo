pipeline {
  agent any

  environment {
    IMAGE_NAME = "ussop2707/jenkins2-repo"
  }

  stages {
    stage('Build') {
      steps {
        sh 'docker build -t $IMAGE_NAME:$BUILD_NUMBER .'
      }
    }

    stage('Push') {
      steps {
        withCredentials([
          usernamePassword(
            credentialsId: 'dockerhub-creds',
            usernameVariable: 'DOCKER_USER',
            passwordVariable: 'DOCKER_PASS'
          )
        ]) {
           sh '''
           echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
           docker push $IMAGE_NAME:$BUILD_NUMBER
           '''
      
    }
  }
}
 }
 }
