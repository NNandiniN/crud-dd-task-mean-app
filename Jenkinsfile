pipeline {
    agent any

    stages {

        stage('Build Images') {
            steps {
                sh 'docker compose build'
            }
        }

        stage('Deploy Cleanly') {
            steps {
                sh '''
                docker compose down --remove-orphans || true
                docker system prune -f || true
                docker compose up -d --force-recreate
                '''
            }
        }
    }
}

