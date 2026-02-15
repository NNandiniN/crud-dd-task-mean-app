pipeline {
    agent any

    stages {

        stage('Build Images') {
            steps {
                sh 'docker compose build'
            }
        }

        stage('Deploy Containers') {
            steps {
                sh '''
                docker compose down || true
                docker compose up -d
                '''
            }
        }
    }
}
