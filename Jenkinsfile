pipeline {
    agent any
    tools { nodejs 'node' }
    environment {
        REACT_APP_DIR = "/var/www/react-app"  // Change this path as needed
        SSH_USER = "rajesh" // Change this to your deployment VM user
        DEPLOYMENT_VM = "13.94.91.224" // Change this to your deployment VM IP
    }
    stages {
        stage('Clone Repository') {
            steps {
                git credentialsId: 'git-credentials', url: 'https://github.com/rajeshprivate007/react-app.git'  // Replace with your repo URL
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('SonarQube Analysis') {
            def scannerHome = tool 'SonarScanner';
            withSonarQubeEnv() {
            sh "${scannerHome}/bin/sonar-scanner"
            }
        }
        stage('Build Application') {
            steps {
                sh 'npm run build'
            }
        }
        stage('Deploy to Server') {
            steps{
                println("Application Deployed")
                // sh 'npm start'
            }
        }
    }
}
