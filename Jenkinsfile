pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                // Checkout your source code from version control
                git 
                
                // Build the code using Maven
                sh 'mvn clean package'
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
}
