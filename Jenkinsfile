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
            sh '''
                sonar-scanner \
                -Dsonar.projectKey=my-poc \
                -Dsonar.sources=. \
                -Dsonar.host.url=http://http://13.127.65.87:9000/
                -Dsonar.login=squ_984b3b2ca344b6a601c5b22a4391b8ea044e2dfb
            '''
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
