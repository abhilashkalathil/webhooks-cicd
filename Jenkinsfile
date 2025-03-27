pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "abhilashkalathil/webhook-cicd-app:latest"
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/abhilashkalathil/webhooks-cicd.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-creds') {
                        docker.image("${DOCKER_IMAGE}").push()
                    }
                }
            }
        }
        stage('Deploy Container') {
            steps {
                sh """
                ssh ubuntu@lab.myc-me.com \
                "docker pull ${DOCKER_IMAGE} && \
                 docker stop my-app || true && \
                 docker rm my-app || true && \
                 ssh ubuntu@your-server-ip "docker ps"
