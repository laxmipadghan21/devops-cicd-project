pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Test') {
            steps {
                echo 'Running application tests...'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t devops-flask-app:latest .'
            }
        }  
        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'laxmipadghan21',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                )]) {
                    sh '''
                        echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
                        docker push laxmipadghan21/devops-flask-app:latest
                        docker logout
                    '''
                }
            }
        }

    }
}