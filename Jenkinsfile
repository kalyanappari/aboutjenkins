pipeline {
    agent any

    environment {
        IMAGE_NAME = 'kalyan3003/aboutjenkins'
        IMAGE_TAG = 'latest'
    }

    stages {

        stage('Clone Repo'){

            steps{
                git branch:'main',url:'https://github.com/kalyanappari/aboutjenkins.git'
            }
        }
        stage('Build') {
            steps {
                bat 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .'
            }
        }
        stage('Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'DockerHUB', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat 'echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin'
                    bat "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }
    }
}
