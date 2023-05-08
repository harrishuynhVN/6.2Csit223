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
    }
}

post {
    always {
        emailext (
            to: 'phuochunghuynh592000@gmail.com',
            subject: "${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
            body: """<p>${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'</p>
                    <p>Check console output at <a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>""",
            attachLog: true
        )
    }
}