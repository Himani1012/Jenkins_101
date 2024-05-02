pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
        NOTIFICATION_EMAIL = 'himanipanday0008@gmail.com'
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
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                    testngResults 'target/testng-results.xml'
                }
            }
        }
        stage('Code Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Security Scan') {
            steps {
                sh 'docker run -v $(pwd):/zap/wrk/:rw -t owasp/zap2docker-weekly zap-baseline.py -t http://localhost:8083'
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    def appSpec = readFile('appspec.yml')
                    def deployOutput = awsCodeDeploy(
                        applicationName: 'your-application-name',
                        deploymentGroupName: 'staging',
                        appSpec: appSpec,
                        revision: 'target/your-artifact.zip'
                    )
                    echo "Deployment ID: ${deployOutput.deploymentId}"
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                // Run integration tests on staging environment
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    def appSpec = readFile('appspec.yml')
                    def deployOutput = awsCodeDeploy(
                        applicationName: 'your-application-name',
                        deploymentGroupName: 'production',
                        appSpec: appSpec,
                        revision: 'target/your-artifact.zip'
                    )
                    echo "Deployment ID: ${deployOutput.deploymentId}"
                }
            }
        }
    }
    post {
        always {
            emailext (
                to: env.NOTIFICATION_EMAIL,
                subject: "Jenkins Pipeline: ${currentBuild.result}",
                body: "Pipeline ${currentBuild.displayName} has finished with status: ${currentBuild.result}",
                attachLog: true
            )
        }
    }
}
