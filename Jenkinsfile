pipeline {
    agent any
    environment {
        DOCKER_HUB_USER = 'tzachaker'
        IMAGE_NAME = 'jenkins-argo-demo'
        IMAGE_TAG = "${env.BUILD_NUMBER}"
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/your-username/jenkins-argo-demo.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_HUB_USER/$IMAGE_NAME:$IMAGE_TAG .'
                sh 'docker tag $DOCKER_HUB_USER/$IMAGE_NAME:$IMAGE_TAG $DOCKER_HUB_USER/$IMAGE_NAME:latest'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-creds', url: '']) {
                    sh 'docker push $DOCKER_HUB_USER/$IMAGE_NAME:$IMAGE_TAG'
                    sh 'docker push $DOCKER_HUB_USER/$IMAGE_NAME:latest'
                }
            }
        }
    }
}
