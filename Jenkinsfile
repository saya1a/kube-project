pipeline {
    agent {label 'kworker1' }

    stages {
        stage('checkout scm') {
            steps {
                script {
                    git branch: 'main', credentialsId: 'kube-proj', url: 'https://github.com/saya1a/kube-project.git'
                }
                stage('Build image') {
                    steps {
                        echo 'Starting to build docker image'
                        script {
                            def customImage = docker.build("myBusyBox:${env.BUILD_ID}")
                        }
                    }
                }
            }
        }
    }
}
