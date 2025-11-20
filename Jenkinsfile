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
        stage('Docker Build') {
            steps {
                sh 'docker build -t node-sample-app:2011 .'
            }
        }
        stage('Docker Run') {
            steps {
                sh 'docker run -d -p 3000:3000 node-sample-app:1411'
            }
        }
    }
    
post {
        always {
            archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true
            logParser(
                useProjectRule: true,
                projectRulePath: '/home/ec2-user/log-parser-rules.txt',
                unstableOnWarning: true,
                failBuildOnError: true
            )
        }
    }
}

}
