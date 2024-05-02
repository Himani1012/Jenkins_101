pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
              // Build the code using Maven
              echo 'mvn clean package'
            }
            
            post {
                success {
                    echo 'Build successful!'
                }
                failure {
                    echo 'Build failed!'
                }
            }
        }
    }
    stage('Unit and Integration Tests') {
              steps {
              }
              
              post {
                  success {
                      echo 'Unit and Integration Tests successful!'
                  }
                  failure {
                      echo 'Unit and Integration Tests failed!'
                  }
              }
          }
   stage('Code Analysis') {
              steps {
              }
              
              post {
                  success {
                      echo 'Code Analysis successful!'
                  }
                  failure {
                      echo 'Code Analysis failed!'
                  }
              }
          }
  stage('Security Scan') {
              steps {
              }
              
              post {
                  success {
                      echo 'Security Scan successful!'
                  }
                  failure {
                      echo 'Security Scan failed!'
                  }
              }
          }
  stage('Deploy to Staging') {
              steps {
              }
              
              post {
                  success {
                      echo 'Deploy to Staging successful!'
                  }
                  failure {
                      echo 'Deploy to Staging failed!'
                  }
              }
          }
  stage('Integration Tests on Staging') {
              steps {
              }
              
              post {
                  success {
                      echo 'Integration Tests on Staging successful!'
                  }
                  failure {
                      echo 'Integration Tests on Staging failed!'
                  }
              }
          }
  stage('Deploy to Production') {
              steps {
              }
              
              post {
                  success {
                      echo 'Deploy to Production successful!'
                  }
                  failure {
                      echo 'Deploy to Production failed!'
                  }
              }
          }
}
