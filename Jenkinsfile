pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                
            }
           
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code...'
                
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
               
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment...'
               
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment...'
               
            }
        }
        post {
    always {
        emailext body: "Pipeline execution finished: ${currentBuild.fullDisplayName}", subject: "Pipeline status: ${currentBuild.currentResult}", to: 'phuochunghuynh592000@gmail.com', attachmentsPattern: '**/*.log'
        }
             }
    }

    
}


