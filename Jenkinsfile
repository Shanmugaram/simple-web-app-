pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                     url: 'https://github.com/Shanmugaram/simple-web-app-.git '
                echo "Code has been checked out."
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
                echo "Dependencies installed."
            }
        }

        stage('Start App') {
            steps {
                sh 'pm2 stop all || true'  // Stop existing instance if any
                sh 'pm2 start index.js'
                echo "Application started."
            }
        }
    }

    post {
        success {
            echo "Build succeeded!"
        }
        failure {
            echo "Build failed!"
        }
    }
}
