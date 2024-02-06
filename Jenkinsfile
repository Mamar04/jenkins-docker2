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
        script {
            // Retrieve Docker Hub credentials
            def credentials = credentials('yhdm')
            if (credentials == null) {
                error('Credentials not found!')
            }
            
            // Extract username and password from credentials
            def username = credentials.username
            def password = credentials.password

            // Login to Docker Hub
            sh "echo '${password}' | docker login -u '${username}' --password-stdin"
        }
    }
}


        stage('Push') {
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
