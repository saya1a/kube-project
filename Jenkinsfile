pipeline {
    agent {label: kworker1-node }

    stages {
        stage('Build and Push Docker Image') {
            steps {
                script {
                    def ecrRepository = 'your-ecr-repository'
                    def imageTag = 'your-image-tag'

                    // Authenticate Docker with ECR
                    def ecrLogin = sh(
                        script: 'aws ecr get-login-password --region your-aws-region | docker login --username AWS --password-stdin your-account-id.dkr.ecr.your-aws-region.amazonaws.com',
                        returnStatus: true
                    )
                    if (ecrLogin == 0) {
                        // Build and tag your Docker image
                        sh "docker build -t ${ecrRepository}:${imageTag} ."

                        // Push the Docker image to ECR
                        sh "docker push ${ecrRepository}:${imageTag}"
                    } else {
                        currentBuild.result = 'FAILURE'
                        error('Failed to log in to ECR')
                    }
                }
            }
        }
    }

    post {
        success {
            // Clean up or additional steps on successful image build and push
        }
    }
}
