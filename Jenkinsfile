pipeline {
   
    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }

    environment {
        DOCKERHUB_CREDENTIALS = credentials('yhdm')
        dockerimagename = "yhdm/jenkins-docker-hub2"
        dockerImage = ""
    }

    stages {
        stage('Build') {
            steps {
                script {
                dockerImage = docker.build jenkins-docker-hub2
                       }
            }
        }

        stage('Push') {
            environment {
               registryCredential = 'yhdm'
           }
              steps{
                 script {
                 docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) { dockerImage.push("latest")
          }
        }
      }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
