pipeline {
    agent {label 'kworker1' }
    environment {
        // Define the image name and tag
        DOCKER_IMAGE = 'mybusybox'
        DOCKER_TAG = '1.1.2'
        // ecr info...
        AWS_DEFAULT_REGION = 'your-aws-regionus-east-1'
        AWS_ACCOUNT_ID = '121247432410'
        ECR_REPOSITORY = 'mykube-repo'
        IMAGE_TAG = '1.1.3'
    }

    stages {
        stage('checkout scm') {
            steps {
                script {
                    git branch: 'main', credentialsId: 'kube-proj', url: 'https://github.com/saya1a/kube-project.git'
                }
            }
        }
        stage('Create ECR Repository') {
            steps {
                script {
                    sh "aws ecr create-repository --repository-name ${ECR_REPOSITORY}"
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    def dockerImage = docker.build("${DOCKER_IMAGE}:${DOCKER_TAG}", "--file Dockerfile .")
                    }
            }
        }
    }
}
