pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                // Checkout your source code from version control
                git 'https://github.com/Himani1012/Jenkins_101.git'
                
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
