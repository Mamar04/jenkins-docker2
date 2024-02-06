pipeline {
    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }

    environment {
        DOCKERHUB_CREDENTIALS = credentials('yhdm')
    }

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t yhdm/jenkins-docker-hub2 .'
            }
        }

        stage('Push') {

           environment {
               registryCredential = 'yhdm'
           }
            steps {
                sh 'docker push yhdm/jenkins-docker-hub2'
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
