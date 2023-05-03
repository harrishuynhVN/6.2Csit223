pipeline {
    agent any
    tools {
        maven 'Maven'
        jdk 'Java'
    }
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
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Security Scan') {
            steps {
                withEnv(['ZAP_PATH=/path/to/zap']) {
                    sh '$ZAP_PATH/zap.sh -cmd -quickurl http://localhost:8080 -quickprogress -outfile /tmp/zap.out'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                sh 'ssh harris@10.141.33.191 "cd /opt/myapp && git pull && mvn clean package && sudo systemctl restart myapp"'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                sh 'jmeter -n -t /path/to/jmeter-test.jmx -l /tmp/jmeter-results.jtl'
            }
        }
        stage('Deploy to Production') {
            steps {
                sh 'ssh harris@10.141.33.191 "cd /opt/myapp && git pull && mvn clean package && sudo systemctl restart myapp"'
            }
        }
    }
    post {
        failure {
            emailext body: "Pipeline failed: ${currentBuild.fullDisplayName}",
                subject: "${currentBuild.fullDisplayName} - Failed",
                to: 'phuochunghuynh592000@gmail.com',
                attachmentsPattern: '/tmp/*.out'
        }
        success {
            emailext body: "Pipeline succeeded: ${currentBuild.fullDisplayName}",
                subject: "${currentBuild.fullDisplayName} - Success",
                to: 'phuochunghuynh592000@gmail.com',
                attachmentsPattern: '/tmp/*.out'
        }
    }
}
