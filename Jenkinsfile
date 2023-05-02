pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                sh 'mvn test'
                sh 'mvn integration-test'
            }
        }
        stage('Code Analysis') {
            steps {
                withMaven(maven: 'maven-3.8.3') {
                    sh 'mvn checkstyle:checkstyle'
                }
            }
        }
        stage('Security Scan') {
            steps {
                sh 'npm install -g snyk'
                sh 'snyk test'
            }
        }
        stage('Deploy to Staging') {
            steps {
                sh 'ssh user@staging-server "cd /path/to/app; git pull"'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                sh 'ssh user@staging-server "cd /path/to/app; mvn integration-test"'
            }
        }
        stage('Deploy to Production') {
            steps {
                sh 'ssh user@production-server "cd /path/to/app; git pull"'
            }
        }
    }
}
