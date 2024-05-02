pipeline {
    agent any
    stages {
        stage('Stage 1: Build') {
            steps {
                sh 'mvn clean package' // Using Maven as the build automation tool
            }
        }
        stage('Stage 2: Unit and Integration Tests') {
            steps {
                sh 'mvn test' // Using Maven for test automation
            }
        }
        stage('Stage 3: Code Analysis') {
            steps {
                sh 'mvn jxr:jxr' // Using the JaCoCo code coverage tool, which can be integrated with Jenkins
            }
        }
        stage('Stage 4: Security Scan') {
            steps {
                sh 'mvn sonar:sonar' // Using the SonarQube tool for security analysis, which can be integrated with Jenkins
            }
        }
        stage('Stage 5: Deploy to Staging') {
            steps {
                sh 'aws s3 cp target/myapp.war s3://mybucket/myapp.war' // Using the AWS CLI to deploy to an S3 bucket
            }
        }
        stage('Stage 6: Integration Tests on Staging') {
            steps {
                sh 'aws s3 cp s3://mybucket/myapp.war myapp.war' // Copy the application from S3 to the staging server
                sh './run-integration-tests.sh' // Run integration tests on the staging environment
            }
        }
        stage('Stage 7: Deploy to Production') {
            steps {
                sh 'aws s3 cp s3://mybucket/myapp.war myapp.war' // Copy the application from S3 to the production server
                sh './deploy-to-production.sh' // Deploy the application to the production server
            }
        }
    }
    post {
        always {
            emailext (
                to: 'himanipanday0008@gmail.com',
                subject: 'Jenkins Pipeline Status',
                body: "The pipeline has completed. \n\n Stage: ${currentStage.name} \n Status: ${currentBuild.currentResult} \n\n Logs: ${env.BUILD_URL}console"
            )
        }
        success {
            emailext (
                to: 'himanipanday0008@gmail.com',
                subject: 'Jenkins Pipeline Success',
                body: "The pipeline has completed successfully. \n\n Stage: ${currentStage.name} \n Status: ${currentBuild.currentResult} \n\n Logs: ${env.BUILD_URL}console"
            )
        }
        failure {
            emailext (
                to: 'himanipanday0008@gmail.com',
                subject: 'Jenkins Pipeline Failure',
                body: "The pipeline has failed. \n\n Stage: ${currentStage.name} \n Status: ${currentBuild.currentResult} \n\n Logs: ${env.BUILD_URL}console"
            )
        }
    }
}
