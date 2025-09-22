pipeline {
    agent any

    tools {
        nodejs 'NodeJS'  // This uses the NodeJS plugin we installed
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm  // Pulls from GitHub
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'  // Windows batch command
            }
        }
        stage('Build') {
            steps {
                bat 'npm run build'  // Creates 'build' folder
            }
        }
        stage('Test') {  // Optional: Run tests if you have them
            steps {
                bat 'npm test -- --watchAll=false'  // Adjust if no tests
            }
        }
        stage('Deploy') {
            steps {
                // Copy build to a local web folder (e.g., C:\deployed-site)
                bat '''
                if not exist "C:\\deployed-site" mkdir C:\\deployed-site
                xcopy /E /Y build C:\\deployed-site
                '''
                echo 'Deployment complete! Serve C:\\deployed-site with: python -m http.server 8000'
            }
        }
    }

    post {
        success {
            echo 'Build and deploy successful!'
        }
        failure {
            echo 'Build failed—check logs.'
        }
    }
}
