pipeline {
  agent any
    environment {
        registry = "eduarte/linux-tweet-app"
        registryCredential = 'dockerhub_id'
        dockerImage = ''
      }

    stages {
      stage('Cloning our Git') {
        steps {
          git 'https://github.com/cloudacia/linux_tweet_app.git'
          }
        }

      stage('Building our image') {
        steps {
          script {
            dockerImage = docker.build registry + ":$BUILD_NUMBER"
            }
          }
        }

        stage('Deploy our image') {
          steps {
            script {
              docker.withRegistry( '', registryCredential ) {
                dockerImage.push()
                }
              }
            }
          }
          
        stage('Cleaning up') {
          steps {
            sh "docker rmi $registry:$BUILD_NUMBER"
            }
          }
        }
      }
