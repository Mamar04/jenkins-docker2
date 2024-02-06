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

stage('Login') {
steps {
sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u
$DOCKERHUB_CREDENTIALS_USR --password-stdin'
}
}

stage('Push') {
steps {

Créer et transférer des images Docker vers Docker Hub à l'aide de
Jenkins Pipeline Référence : EF-TEST-TEST Version : 1

Devops Page 17 sur 32
© EASYFORMER 2016 - Tous droits réservés Date : 31/07/23

sh 'docker push idrisshm/jenkins-docker-hub2'
}
}
}

post {
always {
sh 'docker logout'
}
}
}
