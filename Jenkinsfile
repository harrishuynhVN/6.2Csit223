pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                // Build the code using Maven
                sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                // Run unit tests using JUnit
                sh 'mvn test'
                // Run integration tests using Selenium
                sh 'mvn integration-test'
            }
        }
        stage('Code Analysis') {
            steps {
                // Run code analysis using SonarQube
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Security Scan') {
            steps {
                // Run security scan using OWASP ZAP
                sh 'zap-cli --zap-path /path/to/zap.sh -p 8080 -t http://localhost:8080 -r zap-report.html -x zap-report.xml -J zap-json.log -c zap-config.cfg'
            }
        }
        stage('Deploy to Staging') {
            steps {
                // Deploy to staging using AWS CodeDeploy
                sh 'aws deploy create-deployment --application-name MyApp --deployment-group Staging --s3-location s3://my-bucket/my-app.zip --deployment-config-name CodeDeployDefault.OneAtATime --region us-east-1'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                // Run integration tests on staging using Selenium
                sh 'mvn integration-test -Durl=http://staging.myapp.com'
            }
        }
        stage('Deploy to Production') {
            steps {
                // Deploy to production using AWS CodeDeploy
                sh 'aws deploy create-deployment --application-name MyApp --deployment-group Production --s3-location s3://my-bucket/my-app.zip --deployment-config-name CodeDeployDefault.OneAtATime --region us-east-1'
            }
        }
    }
}
post {
    always {
        emailext body: "Pipeline execution finished: ${currentBuild.fullDisplayName}", subject: "Pipeline status: ${currentBuild.currentResult}", to: 'phuochunghuynh592000@gmail.com', attachmentsPattern: '**/*.log'
    }
}