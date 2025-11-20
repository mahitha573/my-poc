pipeline {
    agent any
    tools {
        nodejs 'NodeJS'  // Ensure NodeJS plugin is installed and configured
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
        stage('Docker Build') {
            steps {
                sh 'docker build -t node-sample-app:2011 .'
            }
        }
        stage('Docker Run') {
            steps {
                sh 'docker run -d -p 3000:3000 node-sample-app:2011'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true
            logParser(
                parsingRulesPath: '/var/lib/jenkins/log-parser-rules.txt', // Global rules
                useProjectRule: true,
                projectRulePath: '/var/lib/jenkins/log-parser-rules.txt', // Project-specific rules
                unstableOnWarning: true,
                failBuildOnError: true
            )
        }
    }
}
