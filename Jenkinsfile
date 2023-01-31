pipeline {
    agent {
        any {
            image 'docker:stable-dind'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('Build and Push Docker Image') {
            steps {
                sh 'cat pwd.txt | docker login -u beyghakymyar --password-stdin'

                sh 'docker-compose build'
                sh 'docker-compose push'
            }
        }
        stage('Deploy on AWS ECR') {
            steps {
                sh 'kubectl apply -f deploy.yaml'
                sh 'kubectl get all'
            }
        }
    }
}
