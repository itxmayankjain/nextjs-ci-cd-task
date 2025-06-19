pipeline {
    agent any

    environment {
        NODE_ENV = 'production'
        PORT = '4000'
    }

    stages {
        stage('Install Dependencies') {
            steps {
                echo 'Installing Node.js dependencies...'
                sh 'npm install'
            }
        }

        stage('Build Next.js App') {
            steps {
                echo 'Building the app...'
                sh 'npm run build'
            }
        }

        stage('Start App with PM2') {
            steps {
                echo 'Starting or restarting the app with PM2...'
                // Ensure PM2 is installed globally
                sh 'npm install -g pm2 || true'

                // Stop old process if exists
                sh 'pm2 delete my-nextjs-app || true'

                // Start new one on port 4000
                sh 'PORT=4000 pm2 start npm --name "my-nextjs-app" -- start'
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful!'
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}

