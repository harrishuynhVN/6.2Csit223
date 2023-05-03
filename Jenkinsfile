pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                sh 'npm run test:unit'
                sh 'npm run test:integration'
            }
        }
        stage('Code Analysis') {
            steps {
                sh 'npm run lint'
            }
        }
        stage('Security Scan') {
            steps {
                sh 'npm audit'
            }
        }
        stage('Deploy to Staging') {
            steps {
                sh 'npm run deploy:staging'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                sh 'npm run test:integration-staging'
            }
        }
        stage('Deploy to Production') {
            steps {
                sh 'npm run deploy:production'
            }
        }
    }

    post {
        always {
            emailext body: "Pipeline execution finished: ${currentBuild.fullDisplayName}", subject: "Pipeline status: ${currentBuild.currentResult}", to: 'phuochunghuynh592000@gmail.com', attachmentsPattern: '**/*.log'
        }
    }
}
