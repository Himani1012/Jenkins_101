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
            stage('Unit and Integration Tests') {
                    steps {
                       
                        echo 'mvn test'
                    }
                    
                   post {
                            success {
                            mail to :"himanipanday0008@gmail.com",
                            subject: "Unit integration tests results",
                            to: true,
                            body:"Test was successful"
                            }    
                            
                        failure {
                            mail to :"himanipanday0008@gmail.com",
                            subject: "Unit integration test results",
                            to: true,
                            body:"Test failed"
                        }
                      
                    
                    }
            }
                
        stage('Code Analysis') {
                    steps {
                        echo 'mvn clean verify sonar:sonar -Dsonar.login=myAuthenticationToken'
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
                        echo 'running sast using sonarqube'
                    }
                    
                    post {
                        success {
                             echo 'Security Scan success!'
                            }
                        
                        failure {
                            echo 'Security Scan failed!'
                        }
                    }
        }
                
        stage('Deploy to Staging') {
                    steps {
                        echo 'eb deploy staging'
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
                        echo 'Run integration tests on staging'
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
                        echo 'eb deploy production'
                    }
                    
                   post {
                            success {
                            mail to :"himanipanday0008@gmail.com",
                            subject: "Results",
                            body:" successful"
                            }    
                            
                        failure {
                            mail to :"himanipanday0008@gmail.com",
                            subject: "Results",
                            body:"failed"
                        }
                      
                    
                    }
        }
}
}
