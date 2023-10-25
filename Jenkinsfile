pipeline {
    agent {label 'kworker1' }
    environment {
        // Define the image name and tag
        DOCKER_IMAGE = 'mybusybox'
        DOCKER_TAG = '1.1.2'
        // ecr info...
        AWS_DEFAULT_REGION = 'us-east-1'
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
        stage('Push to ECR') {
            steps {
                script {
                    // Log in to Amazon ECR
                    //def awsRegion = "${AWS_DEFAULT_REGION}"
                    //def ecrRegistry = "${AWS_ACCOUNT_ID}.dkr.ecr.${awsRegion}.amazonaws.com"
                    //docker.withRegistry("https://${ecrRegistry}", 'ecr:us-east-1') {
                        // Push the Docker image to ECR
                        //dockerImage.push()
                        docker push 121247432410.dkr.ecr.us-east-1.amazonaws.com/mykube-repo:latest
                    }
                }
            }
        }
    }

