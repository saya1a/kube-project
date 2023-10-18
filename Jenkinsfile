pipeline {
    agent {label: kworker1 }

    stages {
        stage('checkout scm') {
            steps {
                script {
                    git branch: 'main', credentialsId: 'trivy', url: 'https://github.com/saya1a/kube-project.git'
                }
            }
        }
    }
}
