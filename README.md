# simple-web-app-

🗂️ Project Structure Overview

simple-web-app/
│
├── index.js                  # Main Node.js file
├── package.json              # Dependencies and scripts
├── views/
│   └── index.html            # Sample HTML page
├── .gitignore
├── Jenkinsfile               # Pipeline as Code
└── README.md

Step 1: Create Your Simple Web App
# On Ubuntu
sudo apt update && sudo apt install nodejs npm -y

Create the app folder and files

mkdir simple-web-app
cd simple-web-app
npm init -y
npm install express

Create index.js:

const express = require('express');
const path = require('path');

const app = express();
const PORT = process.env.PORT || 3000;

app.get('/', (req, res) => {
    res.sendFile(path.join(__dirname, 'views', 'index.html'));
});

app.listen(PORT, () => {
    console.log(`App running on http://54.67.61.58:${PORT}`);
});
**-------------------------------------------------------------------------------------------**

Create views/index.html:

<!DOCTYPE html>
<html>
<head><title>Hello from Jenkins</title></head>
<body>
    <h1>Welcome to your Jenkins-deployed app!</h1>
</body>
</html>

----------------------------------------------------------------------------------------------------

Write Jenkinsfile (Pipeline as Code

pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                     url: 'https://github.com/yourusername/simple-web-app.git '
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

bash
npm install pm2 -g
