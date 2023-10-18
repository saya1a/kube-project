pipeline {
    agent {label 'kworker1'}
    stages {
        stage('build') {
            steps {
                echo 'Build stage'
            }
        }
        stage('Deploy') {
            steps {
                sh 'date'
            }
        }
    }
}
