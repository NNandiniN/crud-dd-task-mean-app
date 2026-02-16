pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/NNandiniN/crud-dd-task-mean-app.git'
            }
        }

        stage('Review') {
            steps {
                sh 'ls -la'
            }
        }

        stage('Package') {
            steps {
                sh 'docker compose build'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker compose down --remove-orphans || true
                docker compose up -d --force-recreate
                '''
            }
        }
    }
}

