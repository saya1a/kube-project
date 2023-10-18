pipeline {
    agent {label 'kworker1' }
    environment {
        // Define the image name and tag
        DOCKER_IMAGE = 'myBusyBox'
        DOCKER_TAG = '1.1.2'
    }

    stages {
        stage('checkout scm') {
            steps {
                script {
                    git branch: 'main', credentialsId: 'kube-proj', url: 'https://github.com/saya1a/kube-project.git'
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    def dockerImage = docker.build("${DOCKER_IMAGE}"${DOCKER_TAG}, "--file Dockerfile .")
                    }
            }
        }
    }
}
