pipeline {
    agent any

    environment {
        COMPOSE_CMD = "docker compose"
    }

    stages {

        stage('Clone') {
            steps {
                echo "Cloning repository..."
                git branch: 'main',
                    url: 'https://github.com/NNandiniN/crud-dd-task-mean-app.git'
            }
        }

        stage('Review') {
            steps {
                echo "Reviewing project structure..."
                sh 'ls -la'
            }
        }

        stage('Build') {
            steps {
                echo "Installing dependencies and building frontend..."

                sh '''
                cd backend
                npm install

                cd ../frontend
                npm install
                npm run build -- --configuration production
                '''
            }
        }

        stage('Test') {
            steps {
                echo "Running backend tests..."

                sh '''
                cd backend
                npm test || true
                '''
            }
        }

        stage('Package') {
            steps {
                echo "Building Docker images..."
                sh '${COMPOSE_CMD} build'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying containers..."
                sh '''
                ${COMPOSE_CMD} down --remove-orphans || true
                ${COMPOSE_CMD} up -d --force-recreate
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment Successful!"
        }
        failure {
            echo "❌ Pipeline Failed. Check logs."
        }
    }
}

