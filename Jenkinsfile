pipeline {
    agent any
    tools {
        nodejs 'NodeJS'  // Name configured in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'poc-10', url: 'https://github.com/mahitha573/my-poc.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'sonar-scanner'
                }
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t node-sample-app:latest .'
            }
        }
    }
}
