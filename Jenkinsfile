pipeline {
  environment {
    registryCredential = 'cloudacia-dev'
    registry = 'eduarte/linux-tweet-app'
    dockerImage = ''
    imageLine = 'docker.io/eduarte/linux-tweet-app'
  }
  agent any
  stages {

    stage('Checkout SCM') {
      steps {
        checkout scm
      }
    }

    stage('Build image') {
      steps {
        script {
            DockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Deploy image') {
      steps {
        script {
          docker.withRegistry( '573869740900.dkr.ecr.us-east-1.amazonaws.com/cloudcia-dev', registryCredential ) {
            DockerImage.push()
          }
        }
      }
    }

    stage('Remove image') {
      steps {
        sh 'docker image rmi $registry:$BUILD_NUMBER'
      }
    }

  //  stage('Anallyze image with Anchore'){
  //    steps {
  //      writeFile file: 'anchore_images', text: imageLine + ":$BUILD_NUMBER"
  //      anchore name: 'anchore_images'
  //    }
  //  }

  //  stage('Pull scanned image') {
  //    steps {
  //      script {
  //        docker.withRegistry( '', registryCredential ) {
  //          image = docker.image(registry + ":$BUILD_NUMBER")
  //          image.pull()
  //        }
  //      }
  //    }
  //  }

  //  stage('Push scanned image') {
  //    steps {
  //      script {
  //        docker.withRegistry( '', registryCredential ) {
  //        image.push('trusted')
  //        }
  //      }
      }
    }
  //}
//}
