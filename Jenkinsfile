pipeline {

    agent any

    environment {

        IMAGE = "mad0008271/mini-gps-backend:latest"
    }

    stages {

        stage('Checkout') {

            steps {
                git 'https://github.com/MADHU871/mini-gps.git'
            }
        }

        stage('Build Image') {

            steps {

                dir('backend') {

                    sh '''
                    docker build -t $IMAGE .
                    '''
                }
            }
        }

        stage('Push Image') {

            steps {

                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {

                    sh '''
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    docker push $IMAGE
                    '''
                }
            }
        }
    }
}