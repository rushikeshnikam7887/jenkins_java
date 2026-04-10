pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "java-hello-app:${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/rushikeshnikam7887/jenkins_java.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    if (fileExists('Dockerfile')) {
                        sh "docker build -t ${DOCKER_IMAGE} ."
                    } else {
                        error "Dockerfile not found!"
                    }
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                sh "docker run --rm ${DOCKER_IMAGE}"
            }
        }
    }

    post {
        success {
            echo 'Build and run successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
