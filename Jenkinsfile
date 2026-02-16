pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/NNandiniN/crud-dd-task-mean-app.git'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker compose down --remove-orphans || true
                docker compose pull
                docker compose up -d
                '''
            }
        }
    }
}

