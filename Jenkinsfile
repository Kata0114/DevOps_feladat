pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = 'registry.example.com'
        DOCKER_IMAGE_TAG = 'latest'
    }

    stages {
        stage('SCM Checkout') {
            steps {
                git 'https://github.com/Kata0114/-Hello-World-http-server---DevOps-feladat.git '
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_REGISTRY/-Hello-World-http-server---DevOps-feladat:$DOCKER_IMAGE_TAG .'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push $DOCKER_REGISTRY/-Hello-World-http-server---DevOps-feladat:$DOCKER_IMAGE_TAG'
            }
        }

        stage('Deploy Application') {
            steps {
                sh 'ssh root@debian "docker pull $DOCKER_REGISTRY/-Hello-World-http-server---DevOps-feladat:$DOCKER_IMAGE_TAG && docker run -d -p 8080:8080 --name myapp $DOCKER_REGISTRY/-Hello-World-http-server---DevOps-feladat:$DOCKER_IMAGE_TAG"'
            }
        }
    }

    post {
        success {
            echo 'sikeres'
        }
        failure {
            echo 'Hiba történt a pipeline futtatása során!'
        }
    }
} 